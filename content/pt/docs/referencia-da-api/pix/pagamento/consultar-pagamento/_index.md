---
title: "Consultando um pagamento realizado"
linkTitle: "Consultando um pagamento realizado"
date: 2021-06-25T14:28:33-03:00
lastmod: 2021-06-25T14:28:33-03:00
weight: 1
draft: false
description: >
  Como consultar pagamentos com Pix enviados
---
---
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/{id}/
```
<br>
Esse endpoint existe para buscar os dados de um pix.

{{% pageinfo %}}
**CONSIDERAÇÕES IMPORTANTES**
- O campo `account` do `target` só é exibido após o pagamento concluir com sucesso
{{% /pageinfo %}}

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
  "account_id": "a5997beb-44ef-438a-ab15-506eaa7fda7e",
  "amount": 28309,
  "approved_at": "2021-06-25T17:46:56Z",
  "approved_by": "user:8c8a97a5-18f3-46fe-94ae-6341d718da8f",
  "confirmed_at": "2021-06-25T17:46:56Z",
  "confirmed_by": "user:65b30ef8-fb55-4ebb-b48a-b01199792b08",
  "created_at": "2021-06-25T17:46:56Z",
  "created_by": "user:8c8a97a5-18f3-46fe-94ae-6341d718da8f",
  "description": "description",
  "end_to_end_id": "E165015552021062517465eeb40dd2f6",
  "failed_at": null,
  "failure_reason_code": null,
  "failure_reason_description": null,
  "fee": 0,
  "id": "e59c23d8-eb3a-4a67-8687-ebfe163211a8",
  "key": null,
  "money_reserved_at": "2021-06-25T17:46:56Z",
  "refunded_amount": 869707,
  "request_id": "aafa7eed-4349-46c2-91ae-7ab4337935cc",
  "settled_at": "2021-06-25T17:46:56Z",
  "source": {
    "account": {
      "account_code": "598461372",
      "account_type": "PG",
      "branch_code": "0001"
    },
    "entity": {"document": "92648457550", "document_type": "cpf", "name": "my name"},
    "institution": {"ispb": "16501555", "name": "Stone Pagamentos S.A."}
  },
  "status": "SETTLED",
  "target": {
    "account": {
      "account_code": "816473259",
      "account_type": "PG",
      "branch_code": "0001"
    },
    "entity": {"document": "***257844**", "document_type": "cpf", "name": "my name"},
    "institution": {"ispb": "34697281", "name": "Outro Banco S.A."}
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

<br>

```
400 Bad Request
```

Acontece quando o id enviado não está em conformidade com o padrão UUID.
