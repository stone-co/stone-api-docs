---
title: "Listar Pix"
linkTitle: "Listar Pix"
date: 2021-06-25T14:28:33-03:00
lastmod: 2021-06-25T14:28:33-03:00
weight: 1
draft: false
description: >
  Como consultar pagamentos com Pix enviados

---
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{account_id}}/pix_payments
```
<br>
Este é um endpoint que unifica Pagamento e devoluções realizadas/recebidas para Participantes Indiretos.
Nele é possível buscar por `chave`, `end_to_end_id` ou `transaction_id` da operação. Os tipos das operações podem ser:

* refund_for_outbound_pix_payment(devolução recebida)
* refund_for_inbound_pix_payment (devolução realizada)
* inbound_pix_payment (pagamento recebido)
* outbound_pix_payment (pagamento realizado)
<br>

#### **PATH PARAMS**

---

**account_id**  `string`

Identificador da conta.

<br>

#### **QUERY PARAMS**

---

**end_to_end_ids**  `string`
<br> Identificador da conta.

**transaction_ids**  `string`
<br> Identificador da conta.

**keys**  `string`
<br> Identificador da conta.

**limit**  `int32`
<br> Limite do cursor.

**before**  `string`
<br> Traz a página anterior ao cursor.

**after**  `string`
<br> Traz a página posterior ao cursor.

<br>
#### **HEADERS**
---
<br>

**authorization*** `string`
<br> Bearer token de autenticação

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
	"cursor": {
		"after": null,
		"before": null,
		"limit": 25
	},
	"data": [{
			"account_id": "d8963f15-20ca-48e9-b033-c12ef88bc0ea",
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
			"key": "ba19c2t8-1aba-47c6-1752-efb2b683213a",
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
				"entity": {
					"document": "92648457550",
					"document_type": "cpf",
					"name": "my name"
				},
				"institution": {
					"ispb": "16501555",
					"name": "Stone Pagamentos S.A."
				}
			},
			"status": "SETTLED",
			"target": {
				"entity": {
					"document": "***257844**",
					"document_type": "cpf",
					"name": "my name"
				},
				"institution": {
					"ispb": "34697281",
					"name": "Outro Banco S.A."
				}
			},
			"transaction_id": null,
			"type": "outbound_pix_payment"
		},
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
			"status": "SETTLED",
			"target_ispb": "16501555",
			"type": "refund_for_inbound_pix_payment"

		},
		{
			"account_id": "d8963f15-20ca-48e9-b033-c12ef88bc0ea",
			"amount": 1010,
			"id": "aa44243f-c8e5-4719-9a6c-9e3d4080bc1d",
			"return_id": "D1650155520210628122786649122226",
			"refund_reason": "beneficiary_request",
			"rejected_at": null,
			"rejection_reason": null,
			"request_id": "d306c427-9eae-9425-bf09-5bdb151d217d",
			"settled_at": "2022-06-29T12:27:27Z",
			"status": "SETTLED",
			"created_at": "2022-06-29T12:27:23Z",
			"outbound_pix_payment_id": "e59c23d8-eb3a-4a67-8687-ebfe163211a8",
			"refund_reason_code": "2",
			"refund_reason_description": "A pessoa que recebeu seu Pix devolveu o valor",
			"type": "refund_for_outbound_pix_payment"
		}
	]
}
```

<br>

```
400 Bad Request
```

```
403 Forbidden
```

```
422 Unprocessable Entity
```

Body
```json
{
  "type": "srn:error:not_indirect_participant"
}
```

Acontece quando a API não é requisitada por um Participante Indireto.



