---
title: "Fluxo de Autorização de Challenge"
linkTitle: "Fluxo de autorização de challenge"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-04-06T18:00:00-03:00
weight: 7
draft: false
description: >
---

---

<br>

Esse fluxo só será solicitado caso você esteja tentando fazer uma transação e receba como resposta o **código 403**. Isso pode acontecer, por exemplo, ao confirmar uma recarga de qualquer tipo.

<br>

#### **Fluxo de autorização de challenge**
---

<br>

1) A requisição que necessita do challenge retornará:

- `status: 403`

```Json
{
	"challenge": {
		"id": id,
		"required_types": ["pin"],
		"type": "srn:error:challenge_required",
		"details": {"error": "challenge_required"}
	}
}
```

Note que `required_types` indicará quais tipos de *credencial* o *subject* deverá preencher pra conseguir uma autorização. Alguns valores possíveis são: `login_password`, `pin` e `totp`.

<br>

2) O próximo *request* deverá conter o `challenge_solution`.

Pra montar o `challenge_solution` você deverá gerar um JWE, onde o valor descriptografado seja um json no seguinte formato:

```Json
{
	"challenge_id": challenge_id, "pin": pin
}
```

O `challenge id` é o valor devolvido no request anterior e segunda chave do json deverá ser o tipo de *credencial* e seu valor correspondente.

Para gerar o JWE você usará a chave com `"use": "enc"` exposta em `api/v1/discovery/keys`. O `protected_header` desse JWE deverá ser algo como `{"alg":"RSA-OAEP","enc":"A256GCM"}`.

Após a solução do *challenge*, você receberá a resposta indicando o status da autorização ou uma resposta com status 403 o problema na solução do *challenge* ou na falta de permissão do *subject*.

<br>

##### **Como gerar um JWE**
---


Para gerar um token JWE (JWT criptografado) seguimos 3 passos:

1) Escrever o conteúdo a ser criptografado (payload). 

2) Buscar a chave pública da Stone, no endpoint /api/v1/discovery/keys, cujo campo "use" seja igual a "enc";

3) Usar uma biblioteca de criptografia passando o payload, a chave pública e o algoritmo utilizado, no caso, RSA-OAEP-256

<br>

Segue um exemplo de como gerar um JWE em Python:

```python
import requests
import json
from jwcrypto import jwe, jwk
import sys
def build_challenge_solution(challenge_id, typ, solution_value):
  dic = {"challenge_id": challenge_id}
  dic.update({typ: solution_value})
  
  return generate_jwe(json.dumps(dic))
  
def generate_jwe(payload):
  key = get_public_key()
  public_key = jwk.JWK()
  public_key = public_key.from_json(json.dumps(key))
  encrypted = jwe.JWE(payload.encode("utf-8"), recipient=public_key, protected={
      "alg": "RSA-OAEP-256",
      "enc": "A256GCM",
      "kid": key["kid"],
  })
  return encrypted.serialize(compact=True)
def get_public_key():
  response = requests.get(
      "https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys")
  for key in response.json()["keys"]:
      if key["use"] == "enc":
          return key
if __name__ == "__main__":
  [challenge_id, typ, value] = sys.argv[1:]
  solution = build_challenge_solution(challenge_id, typ, value)
  print(solution)
```

<br>

##### **Response**

A resposta será um token que será utilizado no challenge.

```
eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiNjdkY2JhZTAtN2JlYi0xMWU5LTllZDUtMDI0MmFjMTEwMDAyIn0.FhyzgGAcmitGYoyzRxO9GhgQ-nMj1DK6gCREmnockGBxjbdPPae7CQPeVzgN50oqt2sK7tEmAMRQxBFAjfsa5bPQT2s-8s3a2M0S01cCwuQJCv43O3EFQoXGv113fGXobEzmyzGY6uAkc6Gmn1CdluN6NfNJIKnplk6GLpgUlrRIrkcEcgPUnJhvhavc-sNK8DUdAT9CaOHyrtZmAsfbmeMc5UdApcM6OJYz1R-4P_92Ygc3WCy2w7vpzwDpHq1z4EjzH7RT9Nxw20CZdi7BWZdgThBWQddikZETB41ghsO_6xOA7GorOl0bvYaSnHrZfVXdbMhltFnKy9WlA_BW66KO2UudkPjLL-SMcM2penwrPXqYMm7z0WIG3hmxH2xYw3TWjED1ZydNgsBH7s14QcAul3TrOS_obHyUrr753o30PTopuFmQesLzoUN0j1qJ6Xm-N2oXdjNEN7TBTXDhbUwgUZLnN_pjtfMT_iSF1imm93REX8w-5Z0rtQ03geORJ48s5ZCF3Gqgj3nKDBk7KLtEUWurpqRoop1EVEgP63ejTpX7kZgxjCAetSyH-pOvXJGZ8Z26Upmy1Rk50keagtr8vMY4raQVMALqWR_yPHiJFWWZNoLvT-3qKOYZS1x--UJP71JIEfeHq9dc-bD_nw_7s9OlqnGKSrQEjvopjY8.n1pAhTkp2N1DAcVE.3DjPqAzJ7SVVM9Tdd-w_UfyvGxtUOAtbQWIVSoz5v6iJ_lwDEkQf1a2EsBvIxTpNLVjdMu_HGFJTYJOmtlN0gM2VZ2YpEtzITw.C_WphE40TvNCXECOLCgGIw
```
<br>





