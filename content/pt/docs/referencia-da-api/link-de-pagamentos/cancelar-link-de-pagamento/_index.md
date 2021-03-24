---
title: "Cancelar um Link de Pagamento"
linkTitle: "Cancelar um Link de Pagamento"
date: 2021-03-15T10::00-03:00
lastmod: 2021-03-15T11:00:00-03:00
weight: 6
description: >
---
---
<br>

Para cancelar um link de pagamento, temos que fechar um pedido, o que vai passar a impedir que qualquer inclusão de item ou novas transações sejam feitas para aquele pedido específico.

{{% pageinfo %}}
**Atenção**

No corpo da requisição deve ser sinalizada a alteração de status para _**canceled**_.

{{% /pageinfo %}}

<br>

```http
PATCH https://sandbox-api.openbank.stone.com.br/api/v1/payment_links/orders/{order_id}/closed
```

##### Body Request

```Json
{
	"account_id": "account_id",
	"status": "canceled"
}
```

##### Response

```Json
{
	"amount": 1000,
	"checkouts": [{
		"accepted_multi_payment_methods": [],
		"accepted_payment_methods": [
			"credit_card"
		],
		"amount": 1000,
		"billing_address": {},
		"billing_address_editable": true,

		"created_at": "2020-05-15T02:06:14Z",
		"credit_card": {
			"authentication": {
				"threed_secure": {},
				"type": "none"
			},
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
				},
				{
					"number": 4,
					"total": 1000
				},
				{
					"number": 5,
					"total": 1000
				},
				{
					"number": 6,
					"total": 1000

				},
				{
					"number": 7,
					"total": 1000
				},
				{
					"number": 8,
					"total": 1000
				},
				{
					"number": 9,
					"total": 1000
				},
				{
					"number": 10,
					"total": 1000
				},
				{
					"number": 11,
					"total": 1000
				},
				{
					"number": 12,
					"total": 1000
				}
			]
		},
		"currency": "BRL",
		"customer": {
			"created_at": "2020-05-07T23:33:15Z",
			"delinquent": false,

			"document": 12345678912,
			"email": "gabriel@email.com",
			"id": "cus_WVbg8Qkc0WIelO4k",
			"name": "Gabriel Tavares",
			"phones": {
				"mobile_phone": {
					"area_code": 21,
					"country_code": 55,
					"number": 987654321
				}
			},
			"type": "individual",
			"updated_at": "2020-05-15T02:02:24Z"
		},
		"customer_editable": true,
		"expires_at": "2020-05-16T02:06:14Z",
		"id": "chk_YMG51zkcyuWz9pXN",
		"metadata": {},
		"payment_url": "https://api.mundipagg.com/checkout/v1/orders/chk_YMG51zkcyuWz9pXN",
		"shippable": false,
		"skip_checkout_success_page": true,
		"status": "open",
		"success_url": "https://sandbox-link.openbank.stone.com.br/t/sucesso",
		"updated_at": "2020-05-15T02:06:14Z"
	}],
	"closed": true,
	"closed_at": "2020-05-15T18:54:35Z",
	"code": "Y0PNSR8FOK",
	"created_at": "2020-05-15T02:06:14Z",

	"currency": "BRL",
	"customer": {
		"created_at": "2020-05-07T23:33:15Z",
		"delinquent": false,
		"document": 12345678912,
		"email": "gabriel@email.com",
		"id": "cus_WVbg8Qkc0WIelO4k",
		"name": "Gabriel Tavares",
		"phones": {
			"mobile_phone": {
				"area_code": 21,
				"country_code": 55,
				"number": 987654321
			}
		},
		"type": "individual",
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
}
```