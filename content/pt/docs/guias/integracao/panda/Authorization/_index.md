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
| resource				| Recurso que sofrerá a ação.   													|
| resource_server 		| Serviço que faz a intermediação para a autorização que foi solicitada ao Panda.	|
| request				| Pedido que um cliente realiza a um servidor.										|



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

Note que `required_types` indicará quais tipos de *credencial* o *subject* deverá preencher pra conseguir uma autorização. Alguns valores possíveis são: `login_password`, `pin`, `totp`, `face_match`


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


#### **Como gerar um JWE**
---


Para gerar um token JWE (JWT criptografado) seguimos 3 passos:

1) Escrever o conteúdo a ser criptografado (payload). 

2) Buscar a chave pública da Stone, no endpoint /api/v1/discovery/keys, cujo campo “use” seja igual a “enc”;

3) Usar uma biblioteca de criptografia passando o payload, a chave pública e o algoritmo utilizado, no caso, RSA-OAEP-256


<br>

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

#### **Request Body**
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


