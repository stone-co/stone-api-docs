---
title: "Criar um pagamento pendente"
linkTitle: "Criar um pagamento pendente"
date: 2021-04-01T18:00:00-03:00
lastmod: 2021-06-25T14:28:33-03:00
weight: 2
draft: false
description: >
---
---
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/outbound_pix_payments
```
<br>

Esse endpoint foi idealizado para criação de um Pix pendente de confirmação enviando os dados do destino ou uma chave Pix.

Ou seja, com este endpoint é possível fazer um pix informando tanto o campo `key` como informando o campo `target`. 

<br>

{{% pageinfo %}}
**CONSIDERAÇÕES IMPORTANTES**

<br>

- O campo `key` se torna obrigatório na presença do campo `transaction_id`.<br>
- A ausência do campo `key`, que seria o envio de um Pix pela Chave Pix torna o campo `target`, que é o campo com os dados bancários do destino, **obrigatório**.<br>
- É possivel criar um Pix somente informando o campo `account_id` sem precisar informar o campo `source`.<br>
- Após a criação do Pix através desse endpoint é necessário confirmar o mesmo através do [endpoint](/docs/referencia-da-api/pix/confirmar-pagamento-pendente/) `/api/v1/pix/outbound_pix_payments/{id}/actions/confirm`. Caso o Pix não seja confirmado, ele permanece no status de `CREATED` até ser confirmado.
- No caso de criação de um Pix utilizando a chave, os dados da `account` do `target` não serão retornados na resposta. Além disso, o campo do `document` do `target` será mascarado caso seja do tipo "cpf".
- Para criar um agendamento de Pix, basta enviar o campo `scheduled_to` com uma data superior ao dia atual.
{{% /pageinfo %}}

<br>

#### **HEADERS**
---
<br>

**authorization*** `string`
<br> Bearer token de autenticação

**x-stone-idempotency-key*** `string`
<br>Chave de idempotência

<br>

Exemplo:

```json
{
  "authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg",
  "x-stone-idempotency-key": "24b53d84-a79d-11eb-bcbc-0242ac130002"
}
```

<br>

#### **BODY PARAMS**
---
<br>

**account_id*** `string`
<br>Identificador da conta

**amount** `integer`
<br>Valor do Pix a ser realizado
<br>Esse campo é opcional na criação do Pix nesse endpoint, desde que este seja informado no endpoint `/api/v1/pix/outbound_pix_payments/{id}/actions/confirm`
<br>Valor mínimo: 0
<br>Valor máximo: 1000000000000

**description** `string`
<br>Descrição do pagamento a ser realizado

**transaction_id** `string`
<br>Identificador da transação, que relaciona uma cobrança a um pagamento Pix. Ela é enviada no response do endpoint `/api/v1/pix/outbound_pix_payments/brcode`
<br>Format: ^[a-zA-Z0-9]{1,25}$|^[a-zA-Z0-9]{26,35}$ 

**key** `string`
<br>Chave identificadora da contraparte
<br>Tamanho mínimo: 0
<br>Tamanho máximo: 77

**scheduled_to** `date`
<br>Data do agendamento
<br>Formato: YYYY-MM-DD (ISO 8601 standard)

**source** <br>Dados do pagador
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**entity**
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**account**
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_type** `string` 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: `PG`, `PP` ou `CC`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_code** `string` 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: ^[1-9]\d{1,19}$
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**branch_code** `string` 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: ^\d{4}$
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**institution**
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**ispb** `string`

**target** <br>Dados da contraparte do pagamento
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**entity**
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**account**
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_type** `string` 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: `PG`, `PP` ou `CC`
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_code** `string` 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: ^[1-9]\d{1,19}$
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**branch_code** `string` 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: ^\d{4}$
  <br>&nbsp;&nbsp;&nbsp;&nbsp;**institution**
  <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**ispb** `string`

<br>
<br>

Body:

```json
{
  "account_id": "477f8576-ca82-462b-bw63-dc28cc6490c3",
  "amount": 39511,
  "description": "some description",
  "transaction_id": "6f4d67a374004257974facecelea4810",
  "key": "+5521999999999",
  "source": {
    "entity": {
      "document": "91098953062",
      "name": "João da Silva"
    },
    "account": {
      "account_type": "CC",
      "account_code": "34",
      "branch_code": "0001"
    },
    "institution": {
      "ispb": "16501555"
    }
  }
}
```

<br>





##### **Responses**

```
201 OK
```

```json
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "amount": 39511,
  "created_at": "2020-12-14T17:38:02Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "description": "some description",
  "transaction_id": "c62153a222df4e60b2e538b068635d41",
  "key": "+5521988040465",
  "end_to_end_id": "E16501555202012141738a87df0acd5f",
  "failed_at": null,
  "failure_reason_code": null,
  "failure_reason_description": null,
  "id": "5b695a22-187a-4181-93c8-811e155a89fc",
  "money_reserved_at": null,
  "refunded_amount": 0,
  "request_id": "1017dbdd97871b98eeaf1c650a20aa15",
  "settled_at": null,
  "scheduled_to": null,
  "source": {
    "account": {
      "account_code": "34",
      "account_type": "CC",
      "branch_code": "0001"
    },
    "entity": {
      "document": "91092573062",
      "document_type": "cpf",
      "name": "João da Silva"
    },
    "institution": {
      "ispb": "16501555",
      "name": "STONE PAGAMENTOS S.A."
    }
  },
  "status": "CREATED",
  "target": {
    "entity": {
      "document": "***369163**",
      "document_type": "cpf",
      "name": "ARCILIO BERNARDI CARDOSO"
    },
    "institution": {
      "ispb": "92894922",
      "name": "BANCO ORIGINAL S.A."
    }
  }
}
```

---

```
400 Bad Request
```
Body

```json
{
  "reason": [
    {"error": "should be at most 77 characters", "path": ["key"]},
    {"error": "must be greater than or equal to 0", "path": ["amount"]},
    {"error": "can't be blank", "path": ["source", "entity", "name"]},
    {"error": "can't be blank", "path": ["target", "entity", "name"]},
    {"error": "must be less than 1_000_000_000_000", "path": ["amount"]},
    {"error": "is invalid", "path": ["account_id"]},
    {"error": "is invalid", "path": ["transaction_id"]},
    {"error": "is invalid", "path": ["key"]},
    {"error": "can't be blank on transaction_id presence", "path": ["key"]},
    {"error": "exceeded one year limit", "path": ["scheduled_to"]}
  ],
  "type": "srn:error:validation"
}
```

Acontece quando são passados campos inválidos. Os erros são cumulativos, então é possível que mais de um motivo de erro seja retornado.

---

```
401 Unauthenticated
```
Body
```json
{  
  "type": "srn:error:unauthenticated"
}
```
Usuário não está autenticado.

<br> 

```
403 Forbidden
```

Body
```json
{  
  "type": "srn:error:unauthorized"
}
```

Usuário não autorizado a realizar a ação.

<br> 

```
422 Unprocessable Entity
```
Body

```json
{
  "type": "srn:error:invalid_key"
}
```

<br>

```json
{
  "type": "srn:error:key_not_found"
}
```

Acontece quando a chave passada não está cadastrada no DICT.

<br>

```json
{
  "type": "srn:error:target_institution_not_found"
}
```

Ocorre quando a outra instituição não existe ou não pertence ao arranjo Pix.

<br>

Body
```json
{
  "type": "srn:error:target_account_not_found"
}
```

Acontece quando o alvo da transferência é uma conta interna, e essa conta interna não existe.
Pagamentos para contas externas inexistentes podem ser criados mas falharão após a confirmação.

<br>

Body
```json
{
  "type": "srn:error:cannot_transfer_to_source_account"
}
```

Acontece quando o alvo da transferência é a conta que está enviando a transferência. Por que você está fazendo isso?

<br>

Body
```json
{
  "type": "srn:error:invoice_amount_differs"
}
```

Acontece quando a transferência está relacionada a uma cobrança criada por uma conta interna, e o valor enviado não corresponde ao valor informado pela cobrança.


<br>

Body
```json
{
  "type": "srn:error:invoice_expired"
}
```

Acontece quando a transferência está relacionada a uma cobrança criada por uma conta interna, e a cobrança expirou.

<br>

Body
```json
{
  "type": "srn:error:invoice_paid"
}
```

Acontece quando a transferência está relacionada a uma cobrança criada por uma conta interna, e a cobrança já foi paga.

----

```
409 Conflict
```

Body
```json
{
  "type": "srn:error:idempotency_conflict"
}
```

Conflito de idempotência. A chave de idempotência já existe para um body diferente.
