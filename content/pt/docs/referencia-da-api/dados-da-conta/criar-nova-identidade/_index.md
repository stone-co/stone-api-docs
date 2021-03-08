---
title: "Criar Nova Identidade"
excerpt: "Cria um novo usuário e sua organização, caso não exista."
hidden: false
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
POST /applications/:client_id/signups
```

---


#### **Authorization**

{{% pageinfo %}}
**oauth2 - authorizationCode**

A autencicação pública deve passar pelo nosso IAM Keycloak através do protocolo OpenID Connect e receber um token JWT.

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


**client_id** `string`

```Json
{
  "type": "object",
  "properties": {
    ":client_id": {
      "type": "string",
      "required": true
    }
  },
  "required": [
    ":client_id"
  ]
}
```


##### **HEADERS**
---

**x-stone-idempotency-key** `string`

**x-stone-subject-token** `string`


```Json
{
  "type": "object",
  "properties": {
    "x-stone-idempotency-key": {
      "type": "string"
    },
    "x-stone-subject-token": {
      "type": "string"
    }
  },
  "required": []
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


##### **Example**
---


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

##### **Schema**
---

**Object:**

 - **document** `string`

 - **document_type** `string`

 - **full_name** `string`

 - **email** `string`


**Organization:** `string` or `Object`

 - **document** `string`

 - **document_type** `string`

 - **full_name** `string`

 - **email** `string`

 - **metadata** `object`

```Json
{
  "type": "object",
  "properties": {
    "user": {
      "type": "object",
      "required": [
        "document",
        "document_type",
        "full_name",
        "email"
      ],
      "properties": {
        "document": {
          "type": "string",
          "format": "cpf"
        },
        "document_type": {
          "type": "string",
          "enum": [
            "cpf"
          ]
        },
        "full_name": {
          "type": "string"
        },
        "email": {
          "type": "string",
          "format": "email"
        }
      }
    },
    "organization": {
      "type": [
        "string",
        "object"
      ],
      "required": [
        "document",
        "document_type"
      ],
      "properties": {
        "document": {
          "type": "string",
          "format": "cnpj"
        },
        "document_type": {
          "type": "string",
          "enum": [
            "cnpj"
          ]
        },
        "full_name": {
          "type": "string"
        },
        "email": {
          "type": "string",
          "format": "email"
        }
      }
    },
    "metadata": {
      "type": "object"
    }
  },
  "required": [
    "user"
  ]
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


##### **Example**
---

```Json
{
  "id": "9c6197d8-4b76-422c-ba81-11fb1ca97313"
}
```


##### **Schema**
---

**Object:**

 - **id** `string`


```Json
 {
  "type": "object",
  "required": [
    "id"
  ],
  "properties": {
    "id": {
      "type": "string",
      "format": "uuid"
    }
  }
}
```

<br>

#### **Send a Test Request**
---


```http
POST https://https://sandbox-api.openbank.stone.com.br/api/v1/applications/:client_id/signups
```

##### **Response Body**

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