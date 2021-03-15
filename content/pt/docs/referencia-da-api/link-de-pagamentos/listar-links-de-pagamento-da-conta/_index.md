---
title: "Listar Links de Pagamentos da Conta"
linkTitle: "Listar Links de Pagamentos da Conta"
date: 2021-03-11T14::00-03:00
lastmod: 2021-03-11T15:00:00-03:00
weight: 3
description: >
---
---

<br>

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/payment_links/{account_id}/orders
```

##### Response

```Json
{
	"data": [{
			"amount": 1000,
			"closed": true,
			"closed_at": "2020-05-15T18:54:35Z",
			"code": "Y0PNSR8FOK",
			"created_at": "2020-05-15T02:06:14Z",
			"currency": "BRL",
			"customer": {
				"created_at": "2020-05-07T23:33:15Z",
				"delinquent": false,
				"document": 12345678912,
				"email": "gabrieltavares@email.com",
				"id": "cus_WVbg8Qkc0WIelO4k",
				"name": "Gabriel Tavares",
				"phones": {
					"mobile_phone": {
						"area_code": 11,
						"country_code": 55,
						"number": 987654321

					}
				},
				"updated_at": "2020-05-15T02:02:24Z"
			},
			"id": "or_djKAl9dacPfB7gBR",
			"items": [{
				"amount": 1000,
				"created_at": "2020-05-15T02:06:14Z",
				"description": "Camisa de malha 100% algodão - Tamanho G - Branca",
				"id": "oi_BQWg5P2FLTlGn97z",
				"quantity": 1,
				"status": "active",
				"type": "product",
				"updated_at": "2020-05-15T02:06:14Z"
			}],
			"status": "canceled",
			"updated_at": "2020-05-15T18:54:35Z"
		},
		{
			"amount": 1000,
			"closed": false,
			"code": "18E1H2I09N",
			"created_at": "2020-05-15T02:04:47Z",
			"currency": "BRL",
			"customer": {
				"created_at": "2020-05-07T23:33:15Z",
				"delinquent": false,
				"document": "09876543201",
				"email": "gabriella@gmail.com",

				"id": "cus_WVbg8Qkc0WIelO4k",
				"name": "Gabriella Pires",
				"phones": {
					"mobile_phone": {
						"area_code": 21,
						"country_code": 55,
						"number": 912345678
					}
				},
				"updated_at": "2020-05-15T02:02:24Z"
			},
			"id": "or_p3EGP2LCdrcvYjq6",
			"items": [{
				"amount": 1000,
				"created_at": "2020-05-15T02:04:47Z",
				"description": "Camisa de malha 100% algodão - Tamanho G - Verde",
				"id": "oi_2X7MD4LFN8sjDE4J",
				"quantity": 1,
				"status": "active",
				"type": "product",
				"updated_at": "2020-05-15T02:04:47Z"
			}],
			"status": "pending",
			"updated_at": "2020-05-15T02:04:47Z"
		}
	],
	"paging": {
		"next": "https://api.mundipagg.com/core/v1/orders?page=2&amp;size=10&amp;navigation=True",
		"total": 2

	}
}
```