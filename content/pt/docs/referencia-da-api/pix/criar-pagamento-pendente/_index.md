---
title: "Criar um pagamento pendente"
linkTitle: "Criar um pagamento pendente"
date: "2021-04-01T18:00:00-03:00"
lastmod: "2021-04-01T18:00:00-03:00"
weight: 2
draft: false
description: >

---

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/outbound_pix_payments
```
Esse endpoint foi idealizado para criação de um Pix pendente de confirmação enviando os dados do destino ou uma chave Pix.

Ao bater na API de criação de um pagamento, o body deve conter OU o campo key com uma chave Pix OU o campo target com os dados do destino.


##### **Header Request**

```Json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

##### **Body Request**

```json
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "amount": 39511,
  "description": "some description",
  "transaction_id": "6f4d67a374004257974facecbdba4810",
  "key": "+5521986758493",
  "source": {
    "entity": {
      "document": "91092573062",
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

##### **Responses**

```http
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
    "account": {
      "account_code": "10510656",
      "account_type": "CC",
      "branch_code": "0001"
    },
    "entity": {
      "document": "04836916313",
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

