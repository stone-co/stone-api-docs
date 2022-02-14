---
title: "Detalhar um Pix realizado"
linkTitle: "Detalhar um Pix realizado"
date: 2021-08-26T10:19:00-03:00
lastmod: 2021-08-26T10:19:00-03:00
weight: 5
draft: false
description: >

---
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/outbound_pix_payments/{{id-do-pix-enviado}}/
```
<br>
Esse endpoint existe para detalhar os dados de um Pix enviado.


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

#### **Responses**

```
200 OK
```

Body:

```json
{
    "account_id": "7e785e98-c859-46c6-9dc7-37ea522ceadf",
    "amount": 1000,
    "approved_at": "2021-08-25T13:23:49Z",
    "approved_by": "application:bcccb1a8-feb8-4eb8-9f24-6babbdba00ba",
    "confirmed_at": "2021-08-25T13:23:49Z",
    "confirmed_by": "application:bcccb1a8-feb8-4eb8-9f24-6babbdba00ba",
    "created_at": "2021-08-25T13:23:24Z",
    "created_by": "application:bcccb1a8-feb8-4eb8-9f24-6babbdba00ba",
    "description": "Teste Pix",
    "end_to_end_id": "E16501555202108251323909dcb109d4",
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "id": "b5c2354c-91a0-4837-bb15-7f88fcd9d4c5",
    "key": null,
    "money_reserved_at": "2021-08-25T13:23:50Z",
    "refunded_amount": 0,
    "request_id": "661c820e7d3a6bc9f9a1c8c8be62559f",
    "settled_at": null,
    "scheduled_to": null,
    "source": {
        "account": {
            "account_code": "88266374",
            "account_type": "PG",
            "branch_code": "0001"
        },
        "entity": {
            "document": "92961229022",
            "document_type": "cpf",
            "name": "Hermione Granger"
        },
        "institution": {
            "ispb": "16501555",
            "name": "Stone Pagamentos S.A."
        }
    },
    "status": "MONEY_RESERVED",
    "target": {
        "account": {
            "account_code": "10023395",
            "account_type": "CC",
            "branch_code": "4104"
        },
        "entity": {
            "document": "***093657**",
            "document_type": "cpf",
            "name": "Luna"
        },
        "institution": {
            "ispb": "90400888",
            "name": "BANCO SANTANDER (BRASIL) S.A."
        }
    },
    "transaction_id": null
}
```

Os possíveis estados do pagamento retornado, que vem no campo `status` são:

- `CREATED`: O pagamento está criado, mas não foi aprovado ainda.
- `CONFIRMED`: O pagamento foi aprovado, mas o dinheiro ainda não saiu da conta.
- `FAILED`: O pagamento falhou.
- `MONEY_RESERVED`: O pagamento foi aprovado, o dinheiro saiu da conta mas ainda não foi concluído.
- `REFUNDED`: O pagamento foi rejeitado pelo outro banco.
- `SETTLED`: O pagamento foi concluído com sucesso.
- `SCHEDULED`: O pagamento foi agendado com sucesso.
- `CANCELLED`: O pagamento agendado foi cancelado.

<br>

```
400 Bad Request
```

Acontece quando o `id` enviado não está em conformidade com o padrão UUID.
