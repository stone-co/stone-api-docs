---
title: "Consultando um pagamento recebido"
linkTitle: "Consultando um pagamento recebido"
date: 2023-09-04T12:10:33-03:00
lastmod: 2023-09-04T12:10:33-03:00
weight: 1
draft: false
description: >
  Como consultar pagamentos com Pix recebidos
---
---
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/inbound_pix_payments/{id}/
```
<br>
Esse endpoint existe para buscar os dados de uma transação Pix recebida.


#### **HEADERS**
---
<br>

**authorization*** `string`
<br> Bearer token de autenticação

<br>

Exemplo:

```json
{
  "authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

<br>

#### **Responses**

```
200 OK
```

Body:

Pagamento associado a QR Code dinâmico imediato

```json
{
  "account_id": "a5997beb-44ef-438a-ab15-506eaa7fda7e",
  "amount": 1000,
  "change_amount": 0,
  "refunded_amount":  123,
  "created_at": "2021-06-25T17:46:56Z",
  "created_by": "user:8c8a97a5-18f3-46fe-94ae-6341d718da8f",
  "description": "description",
  "end_to_end_id": "E165015552021062517465eeb40dd2f6",
  "failed_at": null,
  "pix_payment_invoice_with_due_date": null,
  "pix_payment_static_invoice": null,
  "pix_payment_invoice": {
    "id": "8c9cdf74-4b33-11ee-be56-0242ac120002",
    "additional_data": null,
    "paid_at": "2021-06-25T17:46:56Z"
  },
  "fee": 0,
  "fee_metadata": {
      "fee_type": "fixed",
      "updated_at": "2021-06-25T17:46:56Z",
      "charge_type": null,
      "fixed_value": 0,
      "inserted_at": null,
      "proportional_value": null
  },
  "id": "e59c23d8-eb3a-4a67-8687-ebfe163211a8",
  "purpose": "payment",
  "settled_at": "2021-06-25T17:46:56Z",
  "source": {
    "account": {
      "account_code": "598461372",
      "account_type": "PG",
      "branch_code": "0001"
    },
    "entity": {"document": "91269973045", "document_type": "cpf", "name": "my name"},
    "institution": {"ispb": "16501555", "name": "Stone Pagamentos S.A."}
  },
  "status": "SETTLED",
  "source": {
    "entity": {"document": "***699730**", "document_type": "cpf", "name": "other name"},
    "institution": {"ispb": "34697281", "name": "Outro Banco S.A."}
  },
  "transaction_id": "0d01ec464b3311eebe56-0242ac120002"
}
```
<br>

Pagamento associado a QR Code dinâmico

```json
{
  "account_id": "2749866e-243e-4bdc-8741-250f2088d841",
  "amount": 1000,
  "change_amount": 0,
  "refunded_amount":  123,
  "created_at": "2021-06-25T17:46:56Z",
  "created_by": "user:8c8a97a5-18f3-46fe-94ae-6341d718da8f",
  "description": "description",
  "end_to_end_id": "E165015552021062517465eeb40dd2f6",
  "failed_at": null,
  "pix_payment_invoice": null,
  "pix_payment_static_invoice": null,
  "pix_payment_invoice_with_due_date": {
    "id": "8c9cdf74-4b33-11ee-be56-0242ac120002",
    "additional_data": null,
    "paid_at": "2021-06-25T17:46:56Z"
  },
  "fee": 0,
  "fee_metadata": {
      "fee_type": "fixed",
      "updated_at": "2021-06-25T17:46:56Z",
      "charge_type": null,
      "fixed_value": 0,
      "inserted_at": null,
      "proportional_value": null
  },
  "id": "e59c23d8-eb3a-4a67-8687-ebfe163211a8",
  "purpose": "payment",
  "settled_at": "2021-06-25T17:46:56Z",
  "source": {
    "account": {
      "account_code": "598461372",
      "account_type": "PG",
      "branch_code": "0001"
    },
    "entity": {"document": "91269973045", "document_type": "cpf", "name": "my name"},
    "institution": {"ispb": "16501555", "name": "Stone Pagamentos S.A."}
  },
  "status": "SETTLED",
  "source": {
    "entity": {"document": "***699730**", "document_type": "cpf", "name": "other name"},
    "institution": {"ispb": "34697281", "name": "Outro Banco S.A."}
  },
  "transaction_id": "0221ec464b3311eebe56-0242ac120001"
}
```

<br>

Pagamento associado a QR Code estático

```json
{
  "account_id": "89f127d1-73b0-401b-8289-5b9d9e126f29",
  "amount": 1000,
  "change_amount": 0,
  "refunded_amount":  123,
  "created_at": "2021-06-25T17:46:56Z",
  "created_by": "user:8c8a97a5-18f3-46fe-94ae-6341d718da8f",
  "description": "description",
  "end_to_end_id": "E165015552021062517465eeb40dd2f6",
  "failed_at": null,
  "pix_payment_invoice_with_due_date": null,
  "pix_payment_invoice": null,
  "pix_payment_static_invoice": {
    "id": "8c9cdf74-4b33-11ee-be56-0242ac120002",
    "additional_information": null
  },
  "fee": 0,
  "fee_metadata": {
      "fee_type": "fixed",
      "updated_at": "2021-06-25T17:46:56Z",
      "charge_type": null,
      "fixed_value": 0,
      "inserted_at": null,
      "proportional_value": null
  },
  "id": "e59c23d8-eb3a-4a67-8687-ebfe163211a8",
  "purpose": "payment",
  "settled_at": "2021-06-25T17:46:56Z",
  "source": {
    "account": {
      "account_code": "598461372",
      "account_type": "PG",
      "branch_code": "0001"
    },
    "entity": {"document": "91269973045", "document_type": "cpf", "name": "my name"},
    "institution": {"ispb": "16501555", "name": "Stone Pagamentos S.A."}
  },
  "status": "SETTLED",
  "source": {
    "entity": {"document": "***699730**", "document_type": "cpf", "name": "other name"},
    "institution": {"ispb": "34697281", "name": "Outro Banco S.A."}
  },
  "transaction_id": "1234"
}
```

<br>

```json
401 Unauthorized
```
Body
```json
{
  "type": "srn:error:unauthenticated"
}
```
<br>

```json
403 Forbidden
```
Body
```json
{
  "type": "srn:error:unauthorized"
}
```
<br>
