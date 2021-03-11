---
title: "Verificar Status de Uma Entidade"
excerpt: "Provê um conjunto de informações para acompanhar o pedido de cadastro da conta de pagamento."
hidden: false
date: 2020-05-04T18:32:40-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 2
draft: false
description: >
---

---

Provê um conjunto de informações para acompanhar o pedido de cadastro da conta de pagamento.

---

```http
GET /applications/:client_id/signups/:sign_up_request_id
```


---

#### **Authorization**
---

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

**sign_up_request_id** `string`

```Json
{
  "type": "object",
  "properties": {
    ":client_id": {
      "type": "string",
      "required": true
    },
    ":sign_up_request_id": {
      "type": "string",
      "required": true
    }
  },
  "required": [
    ":client_id",
    ":sign_up_request_id"
  ]
}
```


##### **HEADER**
---

**x-stone-sunject-token** `string`

```Json
{
  "type": "object",
  "properties": {
    "x-stone-subject-token": {
      "type": "string"
    }
  },
  "required": []
}
```

##### **Responses**
---

```Json
200 ok 
```

{{% pageinfo %}}
**A resposta contém os seguintes dados:**

 - id: identificador do pedido de sign up
 - owner_id: identificador do usuário ou organização dona da conta de pagamento
 - owner_type: tipo do dono da conta de pagamento (user ou organization)
 - user_id: id do usuário atrelado a conta de pagamento
 - organization_id: id da organização atrelada a conta de pagamento (pode ser nulo caso seja uma conta apenas de PF).
 - user_email_verified: indica se o usuário está com o e-mail verificado.
 - user_assessment_request_status: status do assessment request para criação do usuário.
 - organization_assessment_request_status: status do assessment request para criação da organização (pode ser nulo caso seja uma conta apenas de PF).
 - subject_id: id da aplicação que criou esse pedido de sign up.
 - status: em qual status está o pedido de sign up created, kyc_analysis(em análise de kyc), finished, failed
 - error: apenas presente caso o status seja failed, contém informações do motivo de falha ao fazer o sign up.
 - metadata: metadados customizados passados ao realizar o cadastro.
 - request_metadata: metadados da requisição de cadastro. Ex: user-agent, ip.
 - resource_details: detalhes envolvendos esse cadastro. Ex: usuário verificou o e-mail, horário que o usuário verificou e-mail, assessment de usuário aprovado, conta de pagamento aberta/fechada/inexistente.
 - resource_type: tipo de recurso principal criado (usuário, organização, conta de pagamento).
 - user: alguns campos do usuário, atualmente só carregamos o id e o approval_status (limited|approved|partially_rejected|pending_analysis).
 - organization: alguns campos da organização, atualmente só carregamos o id e o approval_status.
 - inserted_at: timestamp da criação do pedido de conta de pagamento.
 - updated_at: timestamp da última atualização do pedido de conta de pagamento.

{{% /pageinfo %}}



```Json
{
  "error": null,
  "id": "ea3c66b7-e8cb-46b8-a140-bd6f33738380",
  "inserted_at": "2020-08-11T12:39:53.659803",
  "marketing_data": {
    "utm_adname": null,
    "utm_campaign": null,
    "utm_content": null,
    "utm_medium": null,
    "utm_source": null,
    "utm_term": null
  },
  "metadata": {},
  "organization_id": "3bf2ac6f-2219-4027-8516-d9457f7e6a96",
  "owner_id": "organization:3bf2ac6f-2219-4027-8516-d9457f7e6a96",
  "owner_type": "organization",
  "request_id": "ef53b9b8c8d2dfdf227ee47ca2b9d2ed",
  "request_metadata": {
    "device_generated_id": null,
    "idempotency_key": null,
    "platform_id": null,
    "referer": null,
    "remote_ip": "10.20.201.251, 10.9.2.19",
    "request_id": "ef53b9b8c8d2dfdf227ee47ca2b9d2ed",
    "user_agent": "PostmanRuntime/7.26.1"
  },
  "resource_details": {
    "account_status": "created",
    "account_status_changed_at": "2020-11-26T19:20:10.219377",
    "account_status_timestamp": "2020-11-26T19:20:10.219377",
    "user_automatic_checks_status": "partially_rejected",
    "user_automatic_checks_status_changed_at": "2020-11-26T19:20:10.219377",
    "user_automatic_checks_status_timestamp": "2020-11-25T19:33:14",
    "user_email_verified": true,
    "user_email_verified_changed_at": "2020-11-26T19:20:10.219377",
    "user_email_verified_timestamp": "2020-11-25T19:35:44.770362",
    "user_input_assessment_status": "approved",
    "user_input_assessment_status_changed_at": "2020-11-26T19:20:10.219377",
    "user_input_assessment_status_timestamp": "2020-11-25T19:33:13"
  },
  "resource_type": "srn:resource:paymentaccount",
  "status": "kyc_analysis",
  "subject_id": "user:790081f7-92ce-428f-8334-6443ecc3cbb2",
  "updated_at": "2020-08-11T12:39:56.568580",
  "user_id": "1f4b4f98-f2a2-4ae6-9d4d-2a8dbe5473e1",
  "user": {
    "approval_status": "approved",
    "id": "2d2e6aba-ce11-49be-88c0-0641843cabdc"
  }
}
```


##### **Schema**
---

**Object:**

 - **id** `string`

 - **owner_id** `string`

 - **owner_type** `string`

 - **user_id** `string` 

 - **organization_id** `string`

 - **subject_id** `string`

 - **status** `string`

 - **error** `string` 

 - **matadata** `string`

 - **request_matadata** `string`

 - **insert_at** `string`

 - **update_at** `string` 

**resource_details** `object`

 - **account_status** `boolean` or `string`

 - **account_status_changed_at** `string`

 - **account_status_timestamp** `string`

 - **organization_automatic_checks_status** `string` 

 - **organization_automatic_checks_status_change_at** `string`

 - **organization_automatic_checks_status_timestamp** `string`

 - **organization_input_assessment_status** `string`

 - **organization_input_assessment_status_change_at** `string`

 - **organization_input_assessment_status_timestamp** `string`

 - **user_automatic_checks_status** `string`

 - **user_automatic_checks_status_change_at** `string`

 - **user_automatic_checks_status_timestamp** `string` 

 - **user_input_assessment_status** `string`

 - **user_input_assessment_status_change_at** `string`

 - **user_input_assessment_status_timestamp** `string`

**resource_type** `string`


```Json
{
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    },
    "owner_id": {
      "type": "string"
    },
    "owner_type": {
      "type": "string"
    },
    "user_id": {
      "type": "string"
    },
    "organization_id": {
      "type": "string"
    }, 
    "subject_id": {
      "type": "string"
    },
    "status": {
      "type": "string"
    },
    "error": {
      "type": "string"
    },
    "metadata": {
      "type": "string"
    },
    "request_metadata": {
      "type": "string"
    },
    "inserted_at": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    },
    "resource_details": {
      "type": "object",
      "properties": {
        "account_status": {
          "type": [
            "boolean",
            "string"
          ]
        },
        "account_status_changed_at": {
          "type": "string"
        },
        "account_status_timestamp": {
          "type": "string"
        },
        "organization_automatic_checks_status": {
          "type": "string"
        },
        "organization_automatic_checks_status_changed_at": {
          "type": "string"
        },
        "organization_automatic_checks_status_timestamp": {
          "type": "string"
        },
        "organization_input_assessment_status": {
          "type": "string"
        },
        "organization_input_assessment_status_changed_at": {
          "type": "string"
        },
        "organization_input_assessment_status_timestmap": {
          "type": "string"
        },
        "user_automatic_checks_status": {
          "type": "string"
        },
        "user_automatic_checks_status_changed_at": {
          "type": "string"
        },
        "user_automatic_checks_status_timestamp": {
          "type": "string"
        },
        "user_input_assessment_status": {
          "type": "string"
        },
        "user_input_assessment_status_changed_at": {
          "type": "string"
        },
        "user_input_assessment_status_timestmap": {
          "type": "string"
        }
      }
    },
    "resource_type": {
      "type": "string"
    }
  }
}
```

