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

Esse fluxo será solicitado caso você esteja tentando fazer uma transação e receba como resposta o **código 403**. Isso pode acontecer, por exemplo, ao confirmar uma recarga de qualquer tipo que você não tenha permissão.

<br>

#### **Fluxo de autorização de challenge**
---

<br>

1) A requisição que necessita do challenge retornará:

- `status: 403`

```json
{
    "id": 0,
    "type": "srn:error:challenge_required",
    "challenge": {
        "id": id,
        "required_types": [
            "pin"
        ]
    }
}
```

Note que `required_types` indicará quais tipos de *credencial* o *subject* deverá preencher pra conseguir uma autorização. Alguns valores possíveis são: `login_password`, `pin` e `totp`.

<br>

2) Para seguir o fluxo, o *request* deverá conter o `challenge_solution`.

Pra montar o `challenge_solution` você deverá gerar um [JWE](/docs/referencia-da-api/recargas/fluxo-challenge/#como-gerar-um-jwe), onde o valor descriptografado seja um json no seguinte formato:

```json
{
  "challenge_id": challenge_id,
  "pin": pin
}
```

<br>

O `challenge id` é o valor devolvido no response da requisição anterior que ocasionou o status 403. A segunda chave do json deverá ser o tipo de *credencial* e seu valor correspondente, que no exemplo seria o pin da conta do cliente (ex.: 123456).


<br>

3. Com o resultado do JWE em mãos, realize a requisição desejada acrescentando o atributo x-stone-challenge-solution no header.

###### **Header request**

```json
{
    "authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg",
    "x-stone-idempotency-key": "0001",
    "x-stone-challenge-solution": "81080d67-aac9-415b-868f-4403243201d3"
}
```

<br>

4. Após a solução do *challenge*, você receberá a resposta indicando o status da autorização ou uma resposta com status 403 (problema na solução do *challenge* ou na falta de permissão do *subject*).

<br>

##### **Como gerar um JWE**
---


Para gerar um token JWE (JWT criptografado) seguimos 3 passos:

1) Escrever o conteúdo a ser criptografado (payload).

2) Buscar a chave pública da Stone, no endpoint /api/v1/discovery/keys, cujo campo "use" seja igual a "enc";

3) Usar uma biblioteca de criptografia passando o payload, a chave pública e o algoritmo utilizado, no caso, RSA-OAEP-256. O `protected_header` desse JWE deverá ser algo como `{"alg":"RSA-OAEP","enc":"A256GCM"}`.

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


