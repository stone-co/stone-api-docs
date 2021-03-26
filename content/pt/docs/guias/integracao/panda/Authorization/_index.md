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



#### **Glossário**
---
<br>

| Termo 				| Definição																			|
------------------------|-----------------------------------------------------------------------------------|
| subject				| Quem deseja fazer a ação.     													|
| action				| Ação a ser autorizada.        													|
| resource_id			| Account_id.																		|
| resource_type			| Tipo do Recurso. 																	|
| resource				| Recurso que sofrerá a ação.   													|
| resource_server 		| Responsável por gerenciar o domínio do recurso.									|
| request				| Pedido que um cliente realiza a um servidor.										|

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


#### **Fluxo de autorização de challenge**
---

Caso a action a ser autorizada demande *challenge*, o fluxo seguinte deverá ser seguido:

1) A primeira requisição (com o request body como descrito abaixo) retornará:

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



##### **Como gerar um JWE**
---


Para gerar um token JWE (JWT criptografado) seguimos 3 passos:

1) Escrever o conteúdo a ser criptografado (payload). 

2) Buscar a chave pública da Stone, no endpoint /api/v1/discovery/keys, cujo campo “use” seja igual a “enc”;

3) Usar uma biblioteca de criptografia passando o payload, a chave pública e o algoritmo utilizado, no caso, RSA-OAEP-256

<br>

Segue exemplo de um fluxo de autorização incluindo o challenge:

```Json
{
    "action": {
        "context": {
            "resource_id": "id do recurso",
            "resource_type": "tipo do recurso"
        },
        "name": "nome da action configurada no admin"
    },
    "subject": {
        "token": "jwt da sessão a ser autorizada"
    },
    "context": {
        "user_agent": "user agent",
        "request_hash": "request hash",
        "challenge_solution": "solução do challenge, caso seja necessário",
        "user_ip": "ip do usuário",
        "location": "jwe com lat e long do usuário no momento da autorização"
    }
}
```



##### **Glossário Request Body**
---


##### **Action**

| Campo 				| Descrição														|
------------------------|---------------------------------------------------------------|
| context				| Objeto contendo o id e o tipo do recurso a ser autorizado.    |
| name 					| Nome da Ação.											        |


##### **Subject**

| Campo 				| Descrição																				|
------------------------|---------------------------------------------------------------------------------------|
| token					| Sessão do usário. Deve ser o token presente no momento da requisição a ser autorizada.|
| context				| Objeto contendo informações úteis sobre a sessão ativa.								|


##### **Context**

| Campo 				| Descrição												|
------------------------|-------------------------------------------------------|
| request_hash			| Deve ser um hash do corpo da requisição.				|
| user_agent			| O header de user_agent do subject.					|
| challenge_solution	| JWE com a solução do challenge (caso seja necessário).|


<br>

##### **Schema**
---

**object:**

- **action** `object`

	- **context** `object`

     	- **resource_id** `string`

     	- **resource_type** `string`

    	- **name** `string`


- **subject** `Object`

	- **token** `string`

	- **context** `object`

		- **request_hash** `string`

 		- **user_agent** `string`

 		- **challeng_solution** `string`

 		- **user_ip** `string`

 		- **location** `string`


- **optional_actions** `array[object]`

    - **context** `object`

   		- **resource_id** `string`

   		- **resource_type** `string` 

   		- **name** `string`


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

#### **Tipos de erro**
---

Caso haja algum “problema” durante o processo de autorização, é importante checar o campo `"type"` retornado no response body. 

Abaixo estão listados os types e o que cada um significa.


| Type 								| Campo a qual se refere 							| Status 	| Descrição				|
------------------------------------|---------------------------------------------------| ----------| -----------------------
| srn:error:unauthenticated			| request_body.subject.token						| 401		| A sessão do subject não é válida. |
| srn:error:bad_jwe_token			| request_body.subject.context.challenge_solution	| 403		| JWE (challenge_solution) é inválido. |
| srn:error:unrecognized_key		| request_body.subject.context.challenge_solution	| 403		| JWE criptografado com chave incorreta. |
| srn:error:wrong_challenge_solution| request_body.subject.context.challenge_solution	| 403		| ID do challenge não foi passado na solution. |
| srn:error:bad_challenge_solution	| request_body.subject.context.challenge_solution	| 403		| A resposta do challenge está incorreta. |
| srn:error:challenge_not_found		|request_body.subject.context.challenge_solution	| 403		| O id do challenge não corresponde a nenhum existente. |
| srn:error:unauthorized			| –													| 403		| Subject não tem as permissões necessárias pra executar a ação. |


<br>
