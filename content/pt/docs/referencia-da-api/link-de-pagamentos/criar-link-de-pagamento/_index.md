---
title: "Criar Link de Pagamento"
linkTitle: "Criar Link de Pagamento"
date: 2021-03-15T10::00-03:00
lastmod: 2021-03-15T11:00:00-03:00
weight: 3
description: >
---
---

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A API de Link de Pagamentos fica disponível todos os dias da semana, 24 horas por dia.	
{{< /alert >}}


<br>

---

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/payment_links/orders
```
---
<br>

##### **HEADER**
---

```Json
{
    "authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

<br>

##### **SCHEMA**
---
<br>

* **account_id** `string`<br>
Identificador da conta.
<br>

* **items**:
	
	* **amount** `integer`
	
	* **description** `string`
	
	* **quantity** `integer`

<br>

* **customer**:

	* **name** `string`
	
<br>

* **payments**:

	* **amount** `integer`
	* **payment_method** `string`
	* **checkout**:

		* **expires_in** `integer`
		* **skip_checkout_success_page** `boolean`
		* **billing_address_editable** `boolean`
		* **customer_editable** `boolean`
		* **accepted_payment_methods** `string`
		* **accepted_multi_payment_methods** `string`
		* **success_url** `string`

		* **credit_card** 		
			* **capture** `boolean`

			* **installments** 
				* **number** `integer`
				* **total**  `integer`

<br>	


##### **BODY REQUEST**
---

```Json
{
	"account_id": "c38f9f00-e8f5-487c-b8e0-7b4929bee5db",
	"items": [{
		"amount": 3000,

		"description": "Teste de Link de pagamento.",
		"quantity": 1
	}],
	"customer": {
		"name": "Bruno M R"
	},
	"closed": true,
	"payments": [{
		"amount": 3000,
		"payment_method": "checkout",
		"checkout": {
			"expires_in": 10080,
			"skip_checkout_success_page": true,
			"billing_address_editable": false,
			"customer_editable": true,
			"accepted_payment_methods": [
				"credit_card"
			],
			"accepted_multi_payment_methods": [],
			"success_url": "https://sandbox-link.openbank.stone.com.br/sucesso",
			"credit_card": {
				"capture": true,
				"installments": [{
						"number": 1,
						"total": 1000
					},
					{
						"number": 2,
						"total": 1000
					},
					{
						"number": 3,
						"total": 1000
					}
				]
			}
		}
	}]
}
```
<br>


##### **Response**
---

```Json
{
    "amount": 3000,
    "checkouts": [
        {
            "accepted_multi_payment_methods": [],
            "accepted_payment_methods": [
                "credit_card"
            ],
            "amount": 3000,
            "billing_address": {},
            "billing_address_editable": true,
            "created_at": "2021-06-08T16:54:31Z",
            "credit_card": {
                "authentication": {
                    "threed_secure": {},
                    "type": "none"
                },
                "capture": true,
                "installments": [
                    {
                        "number": 1,
                        "total": 1000
                    },
                    {
                        "number": 2,
                        "total": 1000
                    },
                    {
                        "number": 3,
                        "total": 1000
                    }
                ]
            },
            "currency": "BRL",
            "customer": {
                "created_at": "2021-06-08T16:54:31Z",
                "delinquent": false,
                "id": "cus_GvMY2zgS7c9xYOXD",
                "name": "Bruno M R",
                "phones": {},
                "updated_at": "2021-06-08T16:54:31Z"
            },
            "customer_editable": true,
            "expires_at": "2021-06-15T16:54:31Z",
            "id": "chk_wM3RX3qceulyY6W9",
            "metadata": {},
            "payment_url": "https://stgapi.mundipagg.com/checkout/v1/orders/chk_wM3RX3qceulyY6W9",
            "required_fields": [
                "customer.email",
                "customer.document",
                "customer.mobile_phone",
                "customer.name"
            ],
            "shippable": false,
            "skip_checkout_success_page": true,
            "status": "open",
            "success_url": "https://sandbox-link.openbank.stone.com.br/sucesso",
            "updated_at": "2021-06-08T16:54:31Z"
        }
    ],
    "closed": false,
    "code": "8N5YAPFG2O",
    "created_at": "2021-06-08T16:54:31Z",
    "currency": "BRL",
    "customer": {
        "created_at": "2021-06-08T16:54:31Z",
        "delinquent": false,
        "id": "cus_GvMY2zgS7c9xYOXD",
        "name": "Bruno M R",
        "phones": {},
        "updated_at": "2021-06-08T16:54:31Z"
    },
    "id": "or_ALbmn7RhjAfyzdW7",
    "items": [
        {
            "amount": 3000,
            "created_at": "2021-06-08T16:54:31Z",
            "description": "Teste de Link de pagamento.",
            "id": "oi_x05Y7aPBipcLobae",
            "quantity": 1,
            "status": "active",
            "type": "product",
            "updated_at": "2021-06-08T16:54:31Z"
        }
    ],
    "session_id": "c14e3273-866e-419e-9d8e-ca1801dca662",
    "status": "pending",
    "updated_at": "2021-06-08T16:54:31Z"
}
```