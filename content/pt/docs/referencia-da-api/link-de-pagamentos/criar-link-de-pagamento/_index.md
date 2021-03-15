---
title: "Criar Link de Pagamento"
linkTitle: "Criar Link de Pagamento"
date: 2021-03-15T10::00-03:00
lastmod: 2021-03-15T11:00:00-03:00
weight: 5
description: >
---
---

<br>

```http
POST https://sandbox-api.openbank.stone.com.br/api/v1/payment_links/orders
```

##### Body Request

```Json
{
	"account_id": "436df6e1-1d38-4637-892d-106a5e0b3154",
	"items": [{
		"amount": 13000,

		"description": "Máquina para cortar cabelos sem fio",
		"quantity": 1
	}],
	"customer": {
		"name": "Antonio Brasil de Castro"
	},
	"closed": true,
	"payments": [{
		"amount": 13000,
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
						"total": 13000
					},
					{
						"number": 2,
						"total": 13000
					},
					{
						"number": 3,
						"total": 13000
					}
				]
			}
		}
	}]
}
```

##### Response

```Json
{
	"amount": 13000,
	"checkouts": [{
		"accepted_multi_payment_methods": [],
		"accepted_payment_methods": [
			"credit_card"
		],
		"amount": 13000,
		"billing_address": {},
		"billing_address_editable": true,
		"created_at": "2020-05-15T20:27:36Z",
		"credit_card": {
			"authentication": {
				"threed_secure": {},
				"type": "none"
			},

			"capture": true,
			"installments": [{
					"number": 1,
					"total": 13000
				},
				{
					"number": 2,
					"total": 13000
				},
				{
					"number": 3,
					"total": 13000
				}
			]
		},
		"currency": "BRL",
		"customer": {
			"created_at": "2020-05-15T20:27:35Z",
			"delinquent": false,
			"id": "cus_bvYkAxFVxTLyo8ex",
			"name": "Antonio Brasil de Castro",
			"phones": {},
			"updated_at": "2020-05-15T20:27:35Z"
		},
		"customer_editable": true,
		"expires_at": "2020-05-22T20:27:36Z",
		"id": "chk_WpMBK50cx8hZlnPA",
		"metadata": {},
		"payment_url": "https://api.mundipagg.com/checkout/v1/orders/chk_WpMBK50cx8hZlnPA",

		"shippable": false,
		"skip_checkout_success_page": true,
		"status": "open",
		"success_url": "https://sandbox-link.openbank.stone.com.br/sucesso",
		"updated_at": "2020-05-15T20:27:36Z"
	}],
	"closed": false,
	"code": "R03FYWF3OR",
	"created_at": "2020-05-15T20:27:35Z",
	"currency": "BRL",
	"customer": {
		"created_at": "2020-05-15T20:27:35Z",
		"delinquent": false,
		"id": "cus_bvYkAxFVxTLyo8ex",
		"name": "Antonio Brasil de Castro",
		"phones": {},
		"updated_at": "2020-05-15T20:27:35Z"
	},
	"id": "or_WzqJoA5HnUaLo1YL",
	"items": [{
			"amount": 13000,
			"created_at": "2020-05-15T20:27:35Z",
			"description": "Máquina para cortar cabelos sem fio",
			"id": "oi_534KzWos4xcyNE0v",
			"quantity": 1,
			"status": "active",
			"type": "product",
			"updated_at": "2020-05-15T20:27:35Z"
		}

	],
	"status": "pending",
	"updated_at": "2020-05-15T20:27:36Z"
}
```