---
title: "Criar um devolução de pagamento Pix"
linkTitle: "Criar um devolução de pagamento Pix"
date: 2022-06-29T10:00:00-03:00
lastmod: 2022-06-29T10:00:00-03:00
weight: 2
draft: false
description: >
---
---
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/refunds_for_inbound_pix_payments
```
<br>

Esse endpoint foi idealizado para criação de uma devolução de uma transferência Pix recebida.

<br>

{{% pageinfo %}}
**CONSIDERAÇÕES IMPORTANTES**

<br>

- A transferência Pix recebida deve ser inferior ou igual a 90 dias para realizar a devolução.<br>
- O valor da devolução pode ser igual ou inferior ao valor da transferência original. Caso seja o valor seja inferior, esta será uma devolução parcial, então outras devoluções ainda poderão ser realizadas até que se atinja o valor total.

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

**reason*** `string`
<br> Valores permitidos: `beneficiary_request`

**amount*** `integer`
<br>Valor da devolução a ser realizada
<br>Valor mínimo: 0
<br>Valor máximo: 1000000000000


**inbound_pix_payment_id*** `string`
<br>Identificador da transferência recebida
<br>


Body:

```json
{
  "reason": "beneficiary_request",
  "amount": 39511,
  "inbound_pix_payment_id": "6f4d67a374004257974facecelea4810"
}
```
<br>

##### **Responses**


```
202 OK
```

```json
{
	"account_id": "d8963f15-20ca-48e9-b033-c12ef88bc0ea",
	"amount": 39511,
	"created_at": "2022-06-29T12:27:27Z",
	"created_by": "user:6ead2edf-82f1-4e28-a5f3-f6456508fb02",
	"failed_at": null,
	"failure_reason_code": null,
	"failure_reason_description": null,
	"id": "aa44243f-c8e5-4719-9a6c-9e3d4080bc1d",
	"money_reserved_at": null,
	"reason": "beneficiary_request",
	"request_id": "d306c427-9eae-9425-bf09-5bdb151d217d",
	"return_id": "D1650155520220629122786649111556",
	"reversal_reason": null,
	"reversed_at": null,
	"settled_at": null,
	"source_ispb": "16501555",
	"status": "PENDING",
	"target_ispb": "16501555"
}
```

---

```
400 Bad Request
```

---

```
403 Forbidden
```

---

```
404 Not Found
```

Body
```json
{
  "type": "srn:error:not_found"
}
```
---

```
422 Unprocessable Entity
```

Body
```json
{
  "type": "srn:error:exceeded_avaiable_amount"
}
```

Acontece quando o valor passado excede o valor da transação original.

<br>

Body
```json
{
  "type": "srn:error:inbound_pix_payment_not_settled"
}
```

Tentativa de criar devolução de um pagamento que foi concluída ou aceita.

<br>

Body
```json
{
  "type": "srn:error:refund_period_exceeded"
}
```

O período hábil para criação de uma devolução foi excedido

<br>

Body
```json
{
  "type": "srn:error:target_institution_not_found"
}
```

Acontece quando a devolução é feita para uma Instituição Financeira inexistente ou que não faz mais parte do arranjo Pix.

<br>

---

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

