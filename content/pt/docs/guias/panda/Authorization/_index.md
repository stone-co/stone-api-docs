---
title: "Authorization"
linkTitle: "Authorization"
date: 2021-03-18T09:00:00-03:00
lastmod: 2021-03-18T09:00:00-03:00
weight: 1
description: >
---
---

<br>

O Panda é responsavel por autorizar requisições feitas a outros serviços e suas próprias APIS. Para tal, o mesmo funciona como **PDP (Policy Decision Point)** e **PAP (Policy Administration Point)**.

É possível encontrar a documentação do endpoint de autorização [aqui](https://next.stoplight.io/stoneopenbanking/panda/version%2F1.0/service_api.oas2.yml?view=%2Fauthorization%2Fauthorize-authorization).

Hoje possuímos alguns conceitos importantes para o melhor entendimento da autorização:

- `Action` é o nome da ação que deverá ser autorizada;
- `Context` é todo o conteúdo necessário para a execução da autorização;
- `Challenge` é uma forma de autentição adaptativa que requer um alto nível de confiança no subject;
- `Policies` são regras de autorização (leia mais [aqui](https://next.stoplight.io/stoneopenbanking/panda/version%2F1.0/policy-guide.md));
- O `PDP` é responsável por identicar quais regras devem ser executadas de forma a autorizar a requisição;
- O `PAP` é responsável por administrar as policies e suas regras de autorização;

<br>

#### **PAP**

O panda é capaz de, através do PAP, configurar a execução das autorizações. Para tal o mesmo salva no banco informações como:

- `action` (nome da ação);
- `policies` (lista de ids das policies a serem executadas);
- `context` (contexto exigido na execução das policies);

<br>

**Exemplo:**

```Json
{
	"action": "update_me_public",
	"policies": ["srn:policies:acl", "srn:policies:azp"],
	"context": {
		"scopes": ["entity:write"],
		"azp": ["accounts-hubid@openbank.stone.com.br"]
	}
}
```

<br>

#### **PDP**

Quando o PDP recebe um pedido de autorização  ele verifica a action e seleciona as policies a serem executadas. As policies validam o contexto da requisição, de acordo com a configuração, e executam as verificações necessárias, retornando o resultado `:ok` (authorized) ou `{:error, _error}` (unauthorized).

Para a requisição de autorização os seguites campos são necessários.

- `action` (combinação do nome e o contexto da ação);
- `optional_actions` (lista de ações);
- `subject` (token, tipo e contexto do subject);

<br>

**Exemplo:**

```Json
{
	"action": {
		"context": {
			"resource_id": "d4024146-efea-4b39-bc8c-ecd7428a3c9c",
			"resource_type": "srn:resource:user"
		},
		"name": "update_user_profile"
	},
	"optional_actions": [],
	"subject": {
		"context": {
			"request_hash": "ah61InivM86ghlyqBPrlmdESUBZPtqLLMpYNhn1rTXM",
			"user_agent": "user_agent"
		},
		"token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhenAiOiJhY2NvdW50cy1odWJpZEBvcGVuY...",
		"type": "api"
	}
}
```

{{% pageinfo %}}
**Observações:**

- Em caso de successo parcial (falha em uma `optional_action`) o panda retornará **200** com o erro na `optional_action` que falhou.
- Em caso de challenge ser necessário e não existir resposta o panda retornará **403** com o erro `challenge_required` e as informações necessárias para a resposta do mesmo.

{{% /pageinfo %}}

<br>

##### **Responses**

{{< alert title="200 - ok" >}}
```Json
{
	"action": {
		"name": "update_user_profile",
		"response": "nil",
		"status": "authorized"
	},
	"id": "df6e6811-229b-475e-b07c-76483f30b85e",
	"optional_actions": []
}
```

{{< /alert >}}

{{< alert title="200 - ok (`optional_actions`)" >}}
```Json
{
	"action": {
		"name": "update_user_profile",
		"response": "nil",
		"status": "authorized"
	},
	"id": "aa4d0d91-bac8-4298-a5bf-a4654a038b76",
	"optional_actions": {
		"name": "azp_hubid",
		"response": "nil",
		"status": "authorized"
	}
}
```
{{< /alert >}}


{{< alert title="403 - Forbidden" >}}
```Json
{
	"challenge": "nil",
	"details": {
		"error": "bad_authorize_request"
	},
	"id": "727cd170-31ec-43d0-a9bb-bf1279ca5e59",
	"type": "srn:error:bad_authorize_request"
}
```
{{< /alert >}}


{{< alert title="403 - Forbidden (`challenge required`)" >}}
```Json
{
	"challenge": {
		"id": "c8951702-431c-44bf-981f-4baf984ca2bd",
		"required_types": ["password"]
	},
	"details": {
		"error": "challenge_required"
	},
	"id": "5e876f93-7065-40ec-8bc7-3f46b9649921",
	"type": "srn:error:challenge_required"
}
```
{{< /alert >}}