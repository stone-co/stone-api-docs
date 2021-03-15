---
title: "Criar Nova Identidade"
excerpt: "Cria um novo usuário e sua organização, caso não exista."
date: 2020-05-04T18:32:40-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 1
draft: false
description: >
---

---

Realiza o cadastro de conta de pagamento para pessoa física ou pessoa jurídica.

---
<br>

O cadastro é feito de forma assíncrona de forma a permitir:

 - uma maior velocidade de resposta.
 - resiliência a falhas a partir de retentativas. Com isso conseguimos evitar que erros ocasionais como falhas de infraestrutura afete a nossa retenção de clientes no cadastro.



```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/applications/:client_id/signups
```

---


#### **Authorization**

{{% pageinfo %}}
**oauth2 - authorizationCode**

A autenticação pública deve passar pelo nosso IAM Keycloak através do protocolo OpenID Connect e receber um token JWT.

 - Flow: authorizationCode
 - Authorization URL: https://sandbox-accounts.openbank.stone.com.br
 - Token URL: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token
 - Required Scopes: `stone_subject_id`

{{% /pageinfo %}}

---

#### **Request Parameters**

---

##### **PATH PARAMETER**
---


**client_id*** `string`

```Json
{
  "client_id": "7fc3a55f-b6a3-4b92-a07a-4166bg392341"
}
```


##### **HEADERS**
---

**x-stone-idempotency-key** `string`

**x-stone-subject-token** `string`


```Json
{
  "x-stone-idempotency-key": "25478963571458", 
  "x-stone-subject-token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJhY2NvdW50cy1odWJpZEBvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJuYmYiOjE2MTU0NzI9GjAsInNlc3Npb25fbWV0YWRhdGEiOnsiZW1wcmVzYVpXIjoxLCJjaGF2ZVpXIjoienciLCJwcm9kdWNhbyI6ZmFsc2V9LCJpc3MiOiJkODAzMDQ4ZC03MzA2LTQxNTYtYjNlMS1hNjlkMWNiZjQ3ODEiLCJyZWRpcmVjdF91cmkiOiJodHRwOi8vbG9jYWxob3N0Ojg1ODUvc3RvbmViYW5rL2NvbnNlbnRyZWRpcmVjdCIsInR5cGUiOiJjb25zZW50IiwiZXhwIjoxNjE1NDc5OTI5LCJpYWJ3OjE2MTU0NzI3MTksImp0aSI6Ijk0NTlmMjhhLTQ5NDEtNDA2Zi05YjExLWFmMjdhMWQ2MzEyMCJ9.SptDNxVKp5W_9B"
}
```

<br>

#### **Request Body**

---

Consiste nos dados do usuário e opcionalmente na organização que iremos cadastrar.

Por consistir de dados do usuário que são potencialmente sensíveis, o corpo da requisição deve ser criptografado com o mesmo procedimento utilizado para criptografar o corpo do sign_up público.

O corpo da requisição terá o formato:

```Json
{
    "jwe": "..."
}
```


No exemplo do editor abaixo, forneço o corpo descriptografado da requisição. O campo metadata contém dados customizados que a aplicação desejar salvar no pedido de sign up.


{{% pageinfo %}}
**Observação**

Lembre-se de passar no header *x-stone-idempotency-key* um UUID, isso ajuda que a requisição fique idempotente. Isto é, permite que chame a mesma requisição múltiplas vezes criando apenas um cadastro.
{{% /pageinfo %}}


##### **Schema**
---

**object:**

   - **user*** `object`

     - **document*** `string`

     - **document_type*** `string`

     - **full_name*** `string`

     - **email*** `string`


   - **organization:*** `string` or `Object`

     - **document*** `string`

     - **document_type*** `string`

     - **full_name** `string`

     - **email** `string`

     - **metadata** `object`



##### Example



```Json
{
  "user": {
    "document": "52762077044",
    "document_type": "cpf",
    "full_name": "Fulano da Silva",
    "email": "any_valid_non_burner_email1231@gmail.com"
  },
  "organization": {
    "document": "67946893000133",
    "document_type": "cnpj"
  },
  "metadata": {
    "id_salesperson": "12322"
  }
}
```



##### **Responses**
---

```Json
202 Accepted
```

{{% pageinfo %}}
**Observação**

Por ser uma chamada assíncrona temos como resposta o código de status 202 e o id do pedido de requisição. Esse pode ser utilizado pela API de consulta do pedido de requisição para verificar os metadados e o estado atual do cadastro do cliente.
{{% /pageinfo %}}


##### **Schema**
---

**Object:**

 - **id*** `string`




##### Example


```Json
{
  "id": "9c6197d8-4b76-422c-ba81-11fb1ca97313"
}
```



