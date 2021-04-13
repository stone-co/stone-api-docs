---
title: "Autorizar"
linkTitle: "Autorizar"
date: 2021-03-18T14:00:00-03:00
lastmod: 2021-03-18T14:00:00-03:00
weight: 1
description: >
---
---



```http
POST https://sandbox-api.openbank.stone.com.br/resources/v1/authorization/actions/authorize
```

Esse endpoint tem como finalidade autorizar *actions* de um *subject* sobre um determinado *resource*.

O objetivo de uma autorização é assegurar que o *subject* (pessoa ou aplicação autenticada) possa visualizar, alterar ou deletar um recurso. O fluxo começa no *front-end*, com um *request* cuja ação seja tanto de leitura quanto de escrita. Esse *request* precisa ser encaminhado para o serviço responsável por este recurso. Este serviço é chamado de `resource server`. Ao receber uma requisição que demande autorização, o `resource server` deve perguntar ao panda se o *subject do token* tem ou não autorização para performar aquela ação.

<br>


#### **Quem pode usar esse endpoint?**
---

Apenas `client applications` identificadas como `resource_server` podem solicitar autorizações por esse endpoint. 

Caso não tenha uma aplicação criada em banking ainda, solicite a criação de uma por [aqui](https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o). 

Caso já tenha uma aplicação, é necessário solicitar que a sua aplicação seja definida como um `resource_server`.


<br>

#### **Como gero o token para acessar esse endpoint?**
---

Você pode seguir o guia descrito [clicando aqui](/docs/guias/integracao/autenticacao).


<br>

#### **Glossário**
---

<br>

| Termo                 | Definição                                                                         |
------------------------|-----------------------------------------------------------------------------------|
| subject               | Quem deseja fazer a ação.                                                         |
| action                | Ação a ser autorizada.                                                            |
| resource              | Recurso que sofrerá a ação.                                                       |
| resource_server       | Responsável por gerenciar o domínio do recurso.                                   |
| request               | Pedido que um cliente realiza a um servidor.                                      |

<br>

##### **Campos do objeto Action**

| Campo                 | Descrição                                                     |
------------------------|---------------------------------------------------------------|
| context               | Objeto contendo o id e o tipo do recurso a ser autorizado.    |
| name                  | Nome da Ação.                                                 |
| resource_id           | Account_id.                                                   |
| resource_type         | Tipo do Recurso.                                              |

<br>

##### **Campos do objeto Subject**

| Campo                 | Descrição                                                                             |
------------------------|---------------------------------------------------------------------------------------|
| token                 | Sessão do usário. Deve ser o token presente no momento da requisição a ser autorizada.|
| context               | Objeto contendo informações úteis sobre a sessão ativa.                               |

<br>

##### **Campos do objeto Context**

| Campo                 | Descrição                                             |
------------------------|-------------------------------------------------------|
| request_hash          | Deve ser um hash do corpo da requisição.              |
| user_agent            | O header de user_agent do subject.                    |
| challenge_solution    | JWE com a solução do challenge (caso seja necessário).|

<br>


#### **Fluxo de autorização**
---

Agora que geramos o token para acessar o endpoint, no passo anterior, segue exemplo de um request para solicitar um fluxo de autorização:


##### **Header Request**

```Json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

##### **Body Request**

```json
{
    "action": {
        "context": {
            "resource_id": "1212b12d-8e2e-4661-a6d9-122bb8c46bb2",
            "resource_type": "srn:resource:paymentaccount"
        },
        "name": "show_account_balance_public"
    },
    "subject": {
        "token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJUUUY0c2p5RUJfRUthV0VfSkxEZExHMVlKYXVnNklTV0tQbEdEeG9qNzhjIn0.eyJqdGkiOiIxMjI5NjZmZS04ZDVlLTQ3MGUtOTY3MC0xOTE3N2MyYTU3OTEiLCJleHAiOjE2MTY2OTk3MjIsIm5iZiI6MCwiaWF0IjoxNjE2Njk4ODIyLCJpc3MiOiJodHRwczovL2xvZ2luLnNhbmRib3guc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2FjY291bnQiLCJhdWQiOiJhY2NvdW50Iiwic3ViIjoiMDlhZmI1NWUtYzRmOC00N2NiLWJmOTMtZWM3M2VlY2NiZWJlIiwidHlwIjoiQmVhcmVyIiwiYXpwIjoiYWJjX3dlYkBvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiJhZGM4OTY2ZS1mOGU2LTQ3ZjEtYTU4Yi0zMzg3OThjYTgxNmEiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbImh0dHBzOi8vc2FuZGJveC5jb250YS5zdG9uZS5jb20uYnIiLCJodHRwOi8vbG9jYWxob3N0OjMwMDAiLCJodHRwczovL3NhbmRib3gtZGFzaGJvYXJkLm9wZW5iYW5rLnN0b25lLmNvbS5iciIsImh0dHBzOi8vc2FuZGJveC5vcGVuYmFuay5zdG9uZS5jb20uYnIiXSwic2NvcGUiOiJlbnRpdHk6bGVnYWxfd3JpdGUgZW50aXR5OmxvYW46Y3JlYXRlIGludmVzdG1lbnQ6c3BhY2U6cmVhZCBjYXJkOnJlYWQgaW52ZXN0bWVudDpyZWFkIGVudGl0eTpyZWFkIHByaW5jaXBhbDpjb25zZW50IHBpeDplbnRyeSBpbnZlc3RtZW50OnNwYWNlOmRlcG9zaXQgc3RvbmVfc3ViamVjdF9pZCBlbnRpdHk6bG9hbjphY2NlcHQgcGF5bWVudGFjY291bnQ6KiBpbnZlc3RtZW50OnNwYWNlOndyaXRlIHJlY2VpdmFibGU6YWxsIGV4cGVuZDp0cmFuc2ZlcnM6ZXh0ZXJuYWwgc2FsYXJ5OnBvcnRhYmlsaXR5IGV4cGVuZDpwYXlyb2xscyBwaXg6ZW50cnlfY2xhaW0gcGl4OnBheW1lbnRfaW52b2ljZSBpbnZlc3RtZW50OnNwYWNlOmRlbGV0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOndyaXRlIGV4cGVuZDpib2xldG9pc3N1YW5jZSBleHBlbmQ6cGF5bWVudHMgZW1haWwgaW52ZXN0bWVudDp3cml0ZSBzdG9uZV9hY2NvdW50cyBleHBlbmQ6cmVhZCBwcm9maWxlIGV4cGVuZDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGl4OnBheW1lbnQgcGF5bWVudGFjY291bnQ6cGF5bWVudGxpbmtzOnJlYWQgZXhwZW5kOnBheW1lbnRsaW5rcyBjYXJkOndyaXRlIGludmVzdG1lbnQ6c3BhY2U6d2l0aGRyYXdhbCBleHBlbmQ6cGl4X3BheW1lbnQiLCJlbWFpbF92ZXJpZmllZCI6ZmFsc2UsInN0b25lX3N1YmplY3RfaWQiOiJ1c2VyOmQwMzY5Y2RlLWQ5MjMtNDAzYi05MzgzLWExZTQ1YjU3NTJlMCIsIm5hbWUiOiJCUlVOTyBERSBNRURFSVJPUyBSSUJFSVJPIEJSVU5PIERFIE1FREVJUk9TIFJJQkVJUk8iLCJzdG9uZV9hY2NvdW50cyI6ImVuYWJsZWQiLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJicnVuby5tcmliZWlyb0BzdG9uZS5jb20uYnIiLCJnaXZlbl9uYW1lIjoiQlJVTk8gREUgTUVERUlST1MgUklCRUlSTyIsImxvY2FsZSI6InB0LUJSIiwiZmFtaWx5X25hbWUiOiJCUlVOTyBERSBNRURFSVJPUyBSSUJFSVJPIiwiZW1haWwiOiJicnVuby5tcmliZWlyb0BzdG9uZS5jb20uYnIifQ.GSdzJNpRULNCZoiAP4njh4fog-Swl-REI25KRGA_qKohUf1wWG72YSZtl1VAM5x7CF0mK2oQg_S0jv7CdFQemICsLyt_aKypqOlfgGQTuUmpVQ88uvmSYzNuxjU4rbCp4UpEgygUmHluv7mf_QxfyoAvS5t0VhG0ECC9NrZpduBkJLG5b-IurM3V-YoIr2Er1HsqXcvV559BV9LJze-vKcAgtN6WltkSkWaLOH7D0VZoGX6k0uD3emnFpdcKtbb0eDR5HjfDAAwN-ahCAl7_G40el5fCInXwigyhY1kkzY-DcFlgbsjreSbtH_xA7h_9yKUtwnHJn3IsY-KuffhoOg"
    },
    "context": {}
}
```
<br>

Caso a action não solicite challenge, a resposta do request será essa:



##### **Response**


```json
{
    "action": {
        "name": "show_account_balance_public",
        "response": null,
        "status": "authorized"
    },
    "id": 2772275,
    "optional_actions": []
}
```
<br>

Caso a action a ser autorizada demande *challenge*, o fluxo seguinte deverá ser seguido.

<br>


#### **Fluxo de autorização de challenge**
---

<br>

1) A requisição que necessita do challenge retornará

`status: 403`

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

2) Buscar a chave pública da Stone, no endpoint /api/v1/discovery/keys, cujo campo “use” seja igual a “enc”;

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



```Json
{
    "action": {
        "context": {
            "resource_id": "<inserir resource_id>",
            "resource_type": "srn:resource:user"
        },
        "name": "authorize_action_with_challenge_public"
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


```Json
{
	"action": {
		"name": action_name,
		"status": "authorized",
		optional_actions: []
}
```
<br>

#### **Tipos de erro**
---
<br>

Caso haja algum “problema” durante o processo de autorização, é importante checar o campo `"type"` retornado no response body. 

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


