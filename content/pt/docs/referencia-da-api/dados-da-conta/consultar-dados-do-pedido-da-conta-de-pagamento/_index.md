---
title: "Consultar Dados do Pedido da Conta de Pagamento"
excerpt: "Provê um conjunto de informações para acompanhar o pedido de cadastro da conta de pagamento."
hidden: false
date: 2020-05-04T18:32:40-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 2
draft: false
description: >
---

---
<br>

Provê um conjunto de informações para acompanhar o pedido de cadastro da conta de pagamento.

---


> GET https://sandbox-api.openbank.stone.com.br/api/v1/applications/:client_id/signups/:sign_up_request_id


<br>

#### **Authorization**
---

{{% pageinfo %}}
**oauth2 - authorizationCode**

A autenticação pública deve passar pelo nosso IAM Keycloak através do protocolo OpenID Connect e receber um token JWT.

 - Flow: authorizationCode
 - Authorization URL: https://sandbox-accounts.openbank.stone.com.br
 - Token URL: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token
 - Required Scopes: `stone_subject_id`

{{% /pageinfo %}}

<br>

#### **Request Parameters**

---
<br>

##### **PATH PARAMETER**
---
ID do cliente é o id da sua aplicação para mais informações veja a documentação de [token de acesso](https://docs.openbank.stone.com.br/docs/guias/token-de-acesso/).


O sign up request é o id gerado apartir de um pedido feito via `/singups` para mais informações veja [singup](http://localhost:1313/docs/referencia-da-api/dados-da-conta/criar-nova-conta-de-pagamento/).



**client_id*** `string`

**sign_up_request_id*** `string`

<br>

##### **HEADER**
---

**x-stone-subject-token** `string`

<br>


## Glossário 

- Verificações Automáticas (automatic_checks_assessment): Fazemos verificações automáticas do cadastro de usuário como exemplos, verificar situação cadastral, idade legal, sociedade entre outros.

- KYC Know Your Costumer (user_input_assessment): Validadmos a identidade do usuário após envio de informações como selfie, foto do documato entre outras.

- CHECKS:  Cada informação que pedimos dentro do KYC.

##### **Responses**
---

```
200 ok 
```

{{% pageinfo %}}
**A resposta contém os seguintes dados:**

 - id: identificador do pedido de sign up.
 - account_status: status da conta de pagamento.
    + **created**: conta foi criada.
    + **closed**: conta foi encerrada.
    + **pending_analysis**: pendente de aprovação de KYC.
    + **empty**: Status legado de quando a conta não foi aberta automaticamente.
 - owner_id: identificador do usuário ou organização dona da conta de pagamento.
 - owner_type: tipo do dono da conta de pagamento (user ou organization).
 - user_id: id do usuário atrelado a conta de pagamento.
 - organization_id: id da organização atrelada a conta de pagamento (pode ser nulo caso seja uma conta apenas de PF).
 - user_email_verified: indica se o usuário está com o e-mail verificado.
 - user_assessment_request_status: status resultante da combinação entre os status dos assessments gerados para o usuário nesse pedido.
 - user_input_assessment_status: 
    + **answered**: quando o cliente respondeu KYC e está pendente de análise.
    + **approved**: KYC aprovado.
    + **canceled**: quando o KYC foi cancelado pela operação.
    + **partially_rejected**: Quando pelo menos um dos checks foi aprovado e pelo menos um foi rejeitado.
    + **rejected**:  quando o cadastro for rejeitado por completo.
    + **requested**: quando o KYC ainda não foi respondido. 
    + **undone**: quando a análise do KYC foi desfeita.
 - user_automatic_checks_status: status agrupado das validações automáticas.
    + **approved**: aprovado em todas as validações automáticas.
    + **rejected**: rejeitado o pedido de abertura de conta.
    + **partially_rejected**: Quando foi rejeitado em uma ou mais validações automáticas.
    + **rerunned**: quando reprocessamos as validações.
    + **answered**: status intermediário enquanto as avaliações não foram finalizadas.
    + **canceled**: quando foi cancelado pela operação de analise de KYC.
    + **requested**: quando as validações não foram finalizadas ainda.
 - organization_assessment_request_status: status resultante da combinação entre os status dos assessments gerados para a organização nesse pedido (pode ser nulo caso seja uma conta apenas de PF).
 - subject_id: id da aplicação que criou esse pedido de sign up.
 - status: em qual status está o pedido de sign up: 
     + **created** - pedido criado.
     + **kyc_analysis** - pedido em análise de kyc.
     + **finished** - todas as etapas do pedido finalizadas.
     + **failed** -  pedido falhou no momento da criação.
 - error: apenas presente caso o status seja failed, contém informações do motivo de falha ao fazer o sign up.
 - metadata: metadados customizados passados ao realizar o cadastro.
 - request_metadata: metadados da requisição de cadastro. Ex: user-agent, ip.
 - resource_details: detalhes envolvendos esse cadastro. Ex: usuário verificou o e-mail, horário que o usuário verificou e-mail, assessment de usuário aprovado, conta de pagamento aberta/fechada/inexistente.
 - resource_type: tipo de recurso principal criado.
    + **usuário**: criou uma entidade de usuário (srn:resource:user).
    + **organização**: criou uma entidade de Organização (srn:resource:organization).
    + **conta de pagamento PF**: cria uma entidade usuário com um pedido de conta de pagamento (srn:resource:paymentaccount).
    + **conta de pagamento PJ**: cria uma entidade usuário e organização com pedido de conta de pagamento (srn:resource:paymentaccount).
 - user: alguns campos do usuário, atualmente só carregamos o id e o approval_status (limitedapprovedpartially_rejectedpending_analysis).
 - organization: alguns campos da organização, atualmente só carregamos o id e o approval_status.
 - inserted_at: timestamp da criação do pedido de conta de pagamento.
 - updated_at: timestamp da última atualização do pedido de conta de pagamento.

{{% /pageinfo %}}

<br>

##### **Schema**
---

<br>

**Object:**

 - **id** `string`

 - **owner_id** `string`

 - **owner_type** `string`

 - **owner_document** `string`

 - **user_id** `string` 

 - **user_assessment_request_id** `string`

 - **organization_id** `string`

 - **organization_assessment_request_id** `string`

 - **request_id** `string`

 - **subject_id** `string`

 - **detailed_status** `string`

 - **detailed_status_description** `string`

 - **status** `string`

 - **error** `string` 

 - **matadata** `string`

 - **request_matadata** `string`

 - **insert_at** `string`

 - **update_at** `string` 

 - **resource_details** `object`

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


<br>

##### Example

```json
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
  "owner_document": null,
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
  "detailed_status": "status_111",
  "detailed_status_description": "Conta ainda não foi aberta pois falta o cliente responder informações de cadastro no app",
  "subject_id": "user:790081f7-92ce-428f-8334-6443ecc3cbb2",
  "updated_at": "2020-08-11T12:39:56.568580",
  "user_id": "1f4b4f98-f2a2-4ae6-9d4d-2a8dbe5473e1",
  "user_assessment_request_id": "daa74a8b-701d-405e-b8c4-9976286eeda9"
  "user": {
    "approval_status": "approved",
    "id": "2d2e6aba-ce11-49be-88c0-0641843cabdc"
  }
}
```


#### Possiveis detailed status description

1. Conta não foi aberta para livre movimentação pois o cadastro do cliente foi rejeitado
2. Conta ainda não foi aberta pois está em análise pelo time da conta
3. Estado inconsistente
4. Conta ainda não foi liberada para livre movimentação pois falta o cliente responder informações de cadastro no app e confirmar e-mail
5. Conta não foi aberta pois o cadastro do cliente foi rejeitado
6. Conta ainda não foi liberada para livre movimentação pois falta o cliente verificar o e-mail
7. Conta ainda não foi liberada pois está em análise pelo time da conta
8. Conta encerrada pois o cadastro do cliente foi rejeitado.
9. Conta ainda não foi liberada para livre movimentação pois está pendente análise do time da Conta
10. Conta ainda não foi aberta pois falta o cliente verificar o e-mail
11. Conta não foi liberada para livre movimentação, entrar em contato com o time da Conta
12. Conta não foi liberada para livre movimentação pois o cadastro do cliente foi rejeitado
13. Conta ainda não foi liberada para livre movimentação pois falta o cliente responder informações adicionais de cadastro no app
14. Estado inconsistente
15. Conta ainda não foi liberada para livre movimentação pois falta o cliente responder informações adicionais de cadastro no app e confirmar e-mail
16. Conta aprovada para livre movimentação
17. Conta ainda não foi liberada para livre movimentação pois falta o cliente confirmar e-mail
18. Conta ainda não foi liberada para livre movimentação pois falta o cliente responder novamente informações no app
19. Conta encerrada pois o cadastro do cliente foi rejeitado
20. Conta ainda não foi aberta pois falta o cliente responder informações de cadastro no app e confirmar e-mail
21. Conta ainda não foi liberada para livre movimentação pois falta o cliente responder informações de cadastro no app
22. Conta ainda não foi aberta para livre movimentação pois falta o cliente verificar o e-mail
23. Conta pendente análise pois falta cliente confirmar e-mail
24. Conta ainda não foi aberta pois falta o cliente responder informações de cadastro no app
25. Conta em análise pelo time da conta

> detailed_status é formado por status_número
> ex: `status_1`, `status_111` ...  `status_7559`
