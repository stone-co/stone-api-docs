---
title: "Sign-in (Draft)"
linkTitle: "Sign-in (Draft)"
date: 2021-06-08T16:40:00-03:00
lastmod: 2021-06-08T16:40:00-03:00
draft: true
weight: 2
description: >
---
---



```
POST https://https://sandbox-api.openbank.stone.com.br/api/v1/users/signin
```

Esse endpoint tem como finalidade realizar o sign-in de um usuário.

<br>


#### **Quem pode usar esse endpoint?**
---

Apenas `client applications` identificadas como `resource_server` podem solicitar sign-in por esse endpoint. 

Caso não tenha uma aplicação criada em banking ainda, solicite a criação de uma por [aqui](https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o). 

Caso já tenha uma aplicação, é necessário solicitar que a sua aplicação seja definida como um `resource_server`.


<br>

#### **Como gero o token do header para acessar esse endpoint?**
---

Você pode seguir o guia descrito [clicando aqui](/docs/guias/integracao/autenticacao).


<br>

#### **Glossário**
---

<br>

| Termo                 | Definição                                                           |
------------------------|-------------------------------------------------------------------- |
| client_id             | Id da aplicação autorizada pelo Panda.                              |
| scope | Lista de escopos requisitada para o token.                                          |
| username | Email do usuário.                                                                |
| password | Senha do usuário.                                                                |
| totp | Time-base One-Time Password (token do two factor authentication).                    |
| captcha | Resposta do captcha retornada pelo reCAPTCHA do Google.                           |
| assertion | Identificador da asserção.                                                      |
| assertion_response | Resposta da asserção para sign-in com dispositivo cadastrado.          |
| challenge_id | Identificador do desafio/challenge.                                          |
| challenge_response | Resposta do desafio/challenge para sign-in com dispositivo cadastrado. |
| mobile_app_instance_id | Id retornado pelo firebase.                                        |
| subject               | Quem deseja fazer a ação.                                           |
| action                | Ação a ser autorizada.                                              |
| resource              | Recurso que sofrerá a ação.                                         |
| resource_server       | Responsável por gerenciar o domínio do recurso.                     |
| request               | Pedido que um cliente realiza a um servidor.                        |

<br>

{{% pageinfo %}}
**Atenção!**
Os campos (assertion+assertion_response) e (challenge_id + challenge_response) são mutualmente exclusivos, apenas a presença de um dos pares é aceita.

Para criar o JWE, basta obter as chaves no endpoint /api/v1/discovery/keys, e usar a que possuir a propriedade "use" com valor "enc". Veja mais [aqui](/docs/guias/integracao-para-fornecedores/sign-in-user/#como-gerar-um-jwe)
{{% /pageinfo %}}

<br>


##### **HEADER REQUEST**
---

```json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```
<br>

##### **PARAMS REQUEST**
---
<br>

**device-registration-id*** `string`

**user-agent*** `string`

**platform-id*** `string`

<br>

##### **BODY REQUEST**
--- 

**Payload**
```json
{
  "client_id": "id_cliente",
  "scope": "scope",
  "username": "email",
  "password": "pass",
  "totp": "opcional(string)",
  "captcha": "opcional(string)",
  "assertion": "opcional(string)",
  "assertion_response": "opcional(string)",
  "challenge_id": "opcional(string)",
  "challenge_solution": "opcional(string)",
  "mobile_app_instance_id": "opcional(string)"
}
```
<br>

**Body**
```json
{
  "jwe": "eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiMmI1MDA3OTYtY2M5ZS00NDU5LWJhMGItODYzOTc2MzNlYTlmIn0.IZLW2OOclG_Xy2G1-08RTp_g5x9sjNtq5sbv41iLXuTy9X4W8A5jABydR-OVu1oG7IG_yG47Q9c6w1HZVN-DHPwq1J54t0v4ZFjNj6vuaulqt8V2EZO66cJZT6P0DwAIqhCpM-5OactzWL01WHz_LiWRYr2Z5HXzh5h30bBlpE9yAn4jaZrPh3DANddCAgOVVczQjC6eg4NeXtTleUU6MpcaHfLq6XR1QoweaFD844kP4fy5Xh3UlBObXnpufsY-0LM8Qho-yDPTisSQgs993FDfxCMnnizIDaYe34BoN9m96uhUoIpRTVF0Zbw2IerkDKPSwdDZYZPQ1H-m55cdbL1bTSo45oDlx2vhxaRh7S-ZDqcennsI3adegggzZkRSBxFwcMcruxaDfobysGxGwX_VKsI_EVQjulN2MGDPCc4JBiBZSY-fS9Y6FTUBCiX6OuITsfbhfwLvKncBjU1_OMNFx9X6o0rbsVs63l_meo-0w7de-b0fWa6uXh9vPeWYjjgs1cfoSyeVCxXWJVV0KIhOLtETU3rBz4jD57irg9_oQyqOAkLmA485ZOvP0cIwJ_FC3AqTj3kBoGNUwb9Ka5nK0YsbFSfmT-O_qKUBBAe-CVGm1n1P1dzYdYHrXB0MwdRiHnR9lGwemcLOSrS3sAVtClgaHInbmflgKOXBBn0.8HzuALvH_xURJU2h.bku5VK7c0jL6Dgo7jiDi8rnNkqwK7egi7oEe_ZVkvlt4Xa0IouXcAYzAuciXL_63XBoG29lvLBx9BqyaJzdR69aZVe9ctq7yUCGPiGxMNr8ckFMiMEK0EwUD-ynGFiRvN3PrwJjtjQpJ9drx9kixNyIa49z_kQ2XCWH_cDdMz_sM0u9YjXV_dxwVvFrrL7-EyrRtJ3FrX_RzSmD78dv_.e0pm0IeEhAGPhqq-sM-6ZQ"
}
```


Caso a action não solicite challenge, a resposta do request será essa:



##### **Response**

```
200 OK
```

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJrcGJYREJTZWVNX1hsb0x5RzVwWEdsNmJMTWVSSDZ1S25SZjZLUmVraXJJIn0.eyJqdGkiOiI3OWVmZWZlMS04YWRiLTQwNjAtOThlNy1lMmY3N2I4YWJiNDgiLCJleHAiOjE1ODk5MjYyOTUsIm5iZiI6MCwiaWF0IjoxNTg5OTI1Mzk1LCJpc3MiOiJodHRwczovL2FjY291bnRzLmhvbW9sb2cuc3RvbmUuY3JlZGl0L2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiI5ZTA2NjgyYi02Mzk5LTRkMGItYjEwZC1jMzNlMDVlZDg3MTAiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJob21lYmFua2luZ0BvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiI4OThkMzI1ZS1kNDk3LTQ3N2QtODgyZC01ZjVhZmVkZWQyNzciLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbImh0dHBzOi8vZGFzaGJvYXJkLmhvbW9sb2cuc3RvbmUuY3JlZGl0IiwiaHR0cHM6Ly9ob21lLWJhbmsuaG9tb2xvZy5zdG9uZS5jcmVkaXQiLCJodHRwOi8vbG9jYWxob3N0OjMwMDAiXSwic2NvcGUiOiJjYXJkOnJlYWQgZW50aXR5OnJlYWQgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOnJlYWQgc3RvbmVfc3ViamVjdF9pZCBwYXltZW50YWNjb3VudDppbnN0YW50cGF5bWVudCBwcm9maWxlIGNhcmQ6d3JpdGUgZXhwZW5kOnRyYW5zZmVyczppbnRlcm5hbCBzYWxhcnk6cG9ydGFiaWxpdHkgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOndyaXRlIGV4cGVuZDpib2xldG9pc3N1YW5jZSBleHBlbmQ6cGF5cm9sbHMgZXhwZW5kOmluc3RhbnRwYXltZW50IGVudGl0eTpsZWdhbF93cml0ZSBvZmZsaW5lX2FjY2VzcyBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6KiBleHBlbmQ6cGF5bWVudHMgZXhwZW5kOnRyYW5zZmVyczpleHRlcm5hbCBleHBlbmQ6cGF5bWVudGxpbmtzIGV4cGVuZDpyZWFkIGVtYWlsIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsInN0b25lX3N1YmplY3RfaWQiOiJ1c2VyOjc5MDA4MWY3LTkyY2UtNDI4Zi04MzM0LTY0NDNlY2MzY2JiMiIsIm5hbWUiOiJWaWN0b3IgTmFzY2ltZW50byIsInByZWZlcnJlZF91c2VybmFtZSI6InZpY3Rvci5uYXNjaW1lbnRvQHN0b25lLmNvbS5iciIsImxvY2FsZSI6InB0LUJSIiwiZW1haWwiOiJ2aWN0b3IubmFzY2ltZW50b0BzdG9uZS5jb20uYnIifQ.qa8hgZNCVppTcXBdAaKKXJ9TYxp5FxeDl4cpBh5Dpj7gKfyNVCbbPm8eMWpA5AvNOdccoveOzCHFTFrjPqvFfbgBydLwKhSdfXb6BneHeQVdrGgDgfxeCqGyTJAJpssnqbkSu2WfiZUbjThQfkl7wkwq-irSo-hBLFmb2QTRISuFoESbWUiOSx71QIw7KULEjoOnqC-KerwD18lMGH1_8W_dSYC-IY-C-gKjMoFDcVo2MMh5CpCODPuK1-sX8jEWUNFlE1i6YGMt_6k8twWXovmCUcQmZ1Sgp5vuC7yB-KVHY6nHuYXq28AB0atRVxRYbjjiBCiwLdKFGq-NOCrmsA",
  "expires_in": 900,
  "not-before-policy": 1586206967,
  "refresh_expires_in": 0,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJmZGYzMzVkYy1iZjE1LTQxNDMtOTE2MS0wZDVjYmMzYTk2MmQifQ.eyJqdGkiOiIyZmRkZWY3Ni0yNTllLTQyNTAtOTgwYy03MmI2OWQ5ZjczNDAiLCJleHAiOjAsIm5iZiI6MCwiaWF0IjoxNTg5OTI1Mzk1LCJpc3MiOiJodHRwczovL2FjY291bnRzLmhvbW9sb2cuc3RvbmUuY3JlZGl0L2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJhdWQiOiJodHRwczovL2FjY291bnRzLmhvbW9sb2cuc3RvbmUuY3JlZGl0L2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiI5ZTA2NjgyYi02Mzk5LTRkMGItYjEwZC1jMzNlMDVlZDg3MTAiLCJ0eXAiOiJPZmZsaW5lIiwiYXpwIjoiaG9tZWJhbmtpbmdAb3BlbmJhbmsuc3RvbmUuY29tLmJyIiwiYXV0aF90aW1lIjowLCJzZXNzaW9uX3N0YXRlIjoiODk4ZDMyNWUtZDQ5Ny00NzdkLTg4MmQtNWY1YWZlZGVkMjc3Iiwic2NvcGUiOiJjYXJkOnJlYWQgZW50aXR5OnJlYWQgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOnJlYWQgc3RvbmVfc3ViamVjdF9pZCBwYXltZW50YWNjb3VudDppbnN0YW50cGF5bWVudCBwcm9maWxlIGNhcmQ6d3JpdGUgZXhwZW5kOnRyYW5zZmVyczppbnRlcm5hbCBzYWxhcnk6cG9ydGFiaWxpdHkgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOndyaXRlIGV4cGVuZDpib2xldG9pc3N1YW5jZSBleHBlbmQ6cGF5cm9sbHMgZXhwZW5kOmluc3RhbnRwYXltZW50IGVudGl0eTpsZWdhbF93cml0ZSBvZmZsaW5lX2FjY2VzcyBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6KiBleHBlbmQ6cGF5bWVudHMgZXhwZW5kOnRyYW5zZmVyczpleHRlcm5hbCBleHBlbmQ6cGF5bWVudGxpbmtzIGV4cGVuZDpyZWFkIGVtYWlsIn0.50mSBpXEOysFkaDbRHH4WPINU7d_VeMrvsfBEIPu9RU",
  "scope": "card:read entity:read paymentaccount:paymentlinks:read stone_subject_id paymentaccount:instantpayment profile card:write expend:transfers:internal salary:portability paymentaccount:paymentlinks:write expend:boletoissuance expend:payrolls expend:instantpayment entity:legal_write offline_access entity:write paymentaccount:* expend:payments expend:transfers:external expend:paymentlinks expend:read email",
  "session_state": "898d325e-d497-477d-882d-5f5afeded277",
  "token_type": "bearer"
}
```
<br>

Caso a action demande *challenge*, o fluxo seguinte deverá ser seguido.

<br>


#### **Fluxo de autorização de challenge**
---

<br>

1) A requisição que necessita do challenge retornará

`status: 403`

```json
{
	"challenge": {
		"id": id,
		"required_types": ["pin"],
		"type": "srn:error:challenge_required",
		"details": {"error": "challenge_required"}
	}
}
```

Note que `required_types` indicará quais tipos de *credencial* o *subject* deverá preencher pra conseguir realizar o signin. Alguns valores possíveis são: `login_password`, `pin` e `totp`.

<br>

2) O próximo *request* deverá conter o `challenge_solution`.

Pra montar o `challenge_solution` você deverá gerar um JWE, onde o valor descriptografado seja um json no seguinte formato:

```json
{
    "challenge_id": challenge_id,
    "pin": pin
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

##### **Response**

A resposta será um token que será utilizado no challenge.

```
eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiNjdkY2JhZTAtN2JlYi0xMWU5LTllZDUtMDI0MmFjMTEwMDAyIn0.FhyzgGAcmitGYoyzRxO9GhgQ-nMj1DK6gCREmnockGBxjbdPPae7CQPeVzgN50oqt2sK7tEmAMRQxBFAjfsa5bPQT2s-8s3a2M0S01cCwuQJCv43O3EFQoXGv113fGXobEzmyzGY6uAkc6Gmn1CdluN6NfNJIKnplk6GLpgUlrRIrkcEcgPUnJhvhavc-sNK8DUdAT9CaOHyrtZmAsfbmeMc5UdApcM6OJYz1R-4P_92Ygc3WCy2w7vpzwDpHq1z4EjzH7RT9Nxw20CZdi7BWZdgThBWQddikZETB41ghsO_6xOA7GorOl0bvYaSnHrZfVXdbMhltFnKy9WlA_BW66KO2UudkPjLL-SMcM2penwrPXqYMm7z0WIG3hmxH2xYw3TWjED1ZydNgsBH7s14QcAul3TrOS_obHyUrr753o30PTopuFmQesLzoUN0j1qJ6Xm-N2oXdjNEN7TBTXDhbUwgUZLnN_pjtfMT_iSF1imm93REX8w-5Z0rtQ03geORJ48s5ZCF3Gqgj3nKDBk7KLtEUWurpqRoop1EVEgP63ejTpX7kZgxjCAetSyH-pOvXJGZ8Z26Upmy1Rk50keagtr8vMY4raQVMALqWR_yPHiJFWWZNoLvT-3qKOYZS1x--UJP71JIEfeHq9dc-bD_nw_7s9OlqnGKSrQEjvopjY8.n1pAhTkp2N1DAcVE.3DjPqAzJ7SVVM9Tdd-w_UfyvGxtUOAtbQWIVSoz5v6iJ_lwDEkQf1a2EsBvIxTpNLVjdMu_HGFJTYJOmtlN0gM2VZ2YpEtzITw.C_WphE40TvNCXECOLCgGIw
```
<br>

Segue exemplo de um fluxo de autorização incluindo o challenge:



```json
{
    "action": {
        "context": {
            "resource_id": "<inserir resource_id>",
            "resource_type": "srn:resource:user"
        },
        "name": "action_name"
    },
    "subject": {
        "token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJUUUY0c2p5RUJfRUthV0VfSkxEZExHMVlKYXVnNklTV0tQbEdEeG9qNzhjIn0.eyJqdGkiOiJhM2RhY2MyOC1mNDc0LTQ3YmQtYmNlNS1iNzU4YWEwYmE3YzYiLCJleHAiOjE2MTcxMTM5NzUsIm5iZiI6MCwiaWF0IjoxNjE3MTEzMDc1LCJpc3MiOiJodHRwczovL2xvZ2luLnNhbmRib3guc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2FjY291bnQiLCJhdWQiOiJhY2NvdW50Iiwic3ViIjoiZmMyMjM1ZjgtMzlhYy00Mzk1LTg5YmYtOGY1ZmIzZmU2OTZiIiwidHlwIjoiQmVhcmVyIiwiYXpwIjoiYWJjX3dlYkBvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiI1ZTA1ZTk0My1lYTdmLTRmOGQtODY4NS01MDFkMWVlYTYyZjgiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbImh0dHBzOi8vc2FuZGJveC5jb250YS5zdG9uZS5jb20uYnIiLCJodHRwOi8vbG9jYWxob3N0OjMwMDAiLCJodHRwczovL3NhbmRib3gtZGFzaGJvYXJkLm9wZW5iYW5rLnN0b25lLmNvbS5iciIsImh0dHBzOi8vc2FuZGJveC5vcGVuYmFuay5zdG9uZS5jb20uYnIiXSwic2NvcGUiOiJlbnRpdHk6bGVnYWxfd3JpdGUgZW50aXR5OmxvYW46Y3JlYXRlIGludmVzdG1lbnQ6c3BhY2U6cmVhZCBjYXJkOnJlYWQgaW52ZXN0bWVudDpyZWFkIGVudGl0eTpyZWFkIHByaW5jaXBhbDpjb25zZW50IHBpeDplbnRyeSBpbnZlc3RtZW50OnNwYWNlOmRlcG9zaXQgc3RvbmVfc3ViamVjdF9pZCBlbnRpdHk6bG9hbjphY2NlcHQgcGF5bWVudGFjY291bnQ6KiBpbnZlc3RtZW50OnNwYWNlOndyaXRlIHJlY2VpdmFibGU6YWxsIGV4cGVuZDp0cmFuc2ZlcnM6ZXh0ZXJuYWwgc2FsYXJ5OnBvcnRhYmlsaXR5IGV4cGVuZDpwYXlyb2xscyBwaXg6ZW50cnlfY2xhaW0gcGl4OnBheW1lbnRfaW52b2ljZSBpbnZlc3RtZW50OnNwYWNlOmRlbGV0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOndyaXRlIGV4cGVuZDpib2xldG9pc3N1YW5jZSBleHBlbmQ6cGF5bWVudHMgZW1haWwgaW52ZXN0bWVudDp3cml0ZSBzdG9uZV9hY2NvdW50cyBleHBlbmQ6cmVhZCBwcm9maWxlIGV4cGVuZDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGl4OnBheW1lbnQgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOnJlYWQgZXhwZW5kOnBheW1lbnRsaW5rcyBjYXJkOndyaXRlIGludmVzdG1lbnQ6c3BhY2U6d2l0aGRyYXdhbCBleHBlbmQ6cGl4X3BheW1lbnQiLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwic3RvbmVfc3ViamVjdF9pZCI6InVzZXI6ZGZmOTFiMTEtOTA1YS00YmYzLWFmZTYtMmQxZjgwYjYwMzYxIiwibmFtZSI6IkdhYnJpZWxhIEFicmV1IGRlIEFuZHJhZGUgR2FicmllbGEgQWJyZXUgZGUgQW5kcmFkZSIsInN0b25lX2FjY291bnRzIjoiZW5hYmxlZCIsInByZWZlcnJlZF91c2VybmFtZSI6ImdhYnJpZWxhLmFuZHJhZGVAc3RvbmUuY29tLmJyIiwiZ2l2ZW5fbmFtZSI6IkdhYnJpZWxhIEFicmV1IGRlIEFuZHJhZGUiLCJsb2NhbGUiOiJwdC1CUiIsImZhbWlseV9uYW1lIjoiR2FicmllbGEgQWJyZXUgZGUgQW5kcmFkZSIsImVtYWlsIjoiZ2FicmllbGEuYW5kcmFkZUBzdG9uZS5jb20uYnIifQ.Kf4A_cBnFucisXQYBmH4L70S64l8XQyvzOScqSIOqsG5TIZoX0SFNxjgV3dAi36jiMpZWBWasuWn9xbr1effGzsokGG8r0lvB0kKA4SP72bTSINkqwl3hRzKIRUz-hBPJKuKh6O02jpCaTwnjkpxwyAd7bwMvLrDb9Jqc_aDj_S2kuutzO22z9hV3ao79gDuVp_1N11KWMl1Ye2bnw2-3bBOWlaRjQTSL92KqJdNaGiOlra-xogfguDB8Pb8skJZZdwZBRbk3LcXgOUphrbhiqF0Qdi3VPppkix8o-pp6AytYvGhVyjsXqp-gEyOf4wxt-qSMDuXLnWxiKfantP3Hg",
        "context": {
            "request_hash": "123",
            "user_agent": "postman",
            "user_ip": "<inserir user_ip>",
            "challenge_solution": "eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiNjdkY2JhZTAtN2JlYi0xMWU5LTllZDUtMDI0MmFjMTEwMDAyIn0.FhyzgGAcmitGYoyzRxO9GhgQ-nMj1DK6gCREmnockGBxjbdPPae7CQPeVzgN50oqt2sK7tEmAMRQxBFAjfsa5bPQT2s-8s3a2M0S01cCwuQJCv43O3EFQoXGv113fGXobEzmyzGY6uAkc6Gmn1CdluN6NfNJIKnplk6GLpgUlrRIrkcEcgPUnJhvhavc-sNK8DUdAT9CaOHyrtZmAsfbmeMc5UdApcM6OJYz1R-4P_92Ygc3WCy2w7vpzwDpHq1z4EjzH7RT9Nxw20CZdi7BWZdgThBWQddikZETB41ghsO_6xOA7GorOl0bvYaSnHrZfVXdbMhltFnKy9WlA_BW66KO2UudkPjLL-SMcM2penwrPXqYMm7z0WIG3hmxH2xYw3TWjED1ZydNgsBH7s14QcAul3TrOS_obHyUrr753o30PTopuFmQesLzoUN0j1qJ6Xm-N2oXdjNEN7TBTXDhbUwgUZLnN_pjtfMT_iSF1imm93REX8w-5Z0rtQ03geORJ48s5ZCF3Gqgj3nKDBk7KLtEUWurpqRoop1EVEgP63ejTpX7kZgxjCAetSyH-pOvXJGZ8Z26Upmy1Rk50keagtr8vMY4raQVMALqWR_yPHiJFWWZNoLvT-3qKOYZS1x--UJP71JIEfeHq9dc-bD_nw_7s9OlqnGKSrQEjvopjY8.n1pAhTkp2N1DAcVE.3DjPqAzJ7SVVM9Tdd-w_UfyvGxtUOAtbQWIVSoz5v6iJ_lwDEkQf1a2EsBvIxTpNLVjdMu_HGFJTYJOmtlN0gM2VZ2YpEtzITw.C_WphE40TvNCXECOLCgGIw"
        }
    }
}
```
<br>

##### **Responses**
---


- **200 OK**


```json
{
  "action": {
    "name": "action_name",
    "status": "authorized",
    "optional_actions": []
  }
}
```
<br>

#### **Tipos de erro**
---
<br>

Caso haja algum "problema" durante o processo de signin, é importante checar o campo `"type"` retornado no response body. 

Abaixo estão listados os types e o que cada um significa.

<br>

| Type 								| Campo a qual se refere 							| Status 	| Descrição				|
------------------------------------|---------------------------------------------------| ----------| -----------------------
| srn:error:unauthenticated			| request_body.subject.token						| 401		| A sessão do subject não é válida. |
| srn:error:bad_jwe_token			| request_body.subject.context.challenge_solution	| 403		| JWE (challenge_solution) é inválido. |
| srn:error:unrecognized_key		| request_body.subject.context.challenge_solution	| 403		| JWE criptografado com chave incorreta. |
| srn:error:wrong_challenge_solution| request_body.subject.context.challenge_solution	| 403		| ID do challenge não foi passado na solution. |
| srn:error:bad_challenge_solution	| request_body.subject.context.challenge_solution	| 403		| A resposta do challenge está incorreta. |
| srn:error:challenge_not_found		|request_body.subject.context.challenge_solution	| 403		| O id do challenge não corresponde a nenhum existente. |
| srn:error:unauthorized			| –													| 403		| Subject não tem as permissões necessárias pra executar a ação. |


