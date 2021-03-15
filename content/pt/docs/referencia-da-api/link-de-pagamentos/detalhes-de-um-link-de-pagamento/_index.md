---
title: "Detalhes de um Link de Pagamento"
linkTitle: "Detalhes de um Link de Pagamento"
date: 2021-03-15T10::00-03:00
lastmod: 2021-03-15T15:00:00-03:00
weight: 4
description: >
---
---

<br>

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/payment_links/{account_id}/orders/{order_id}
```

##### Response

```Json
{
	"amount": 1000,
	"charges": [{
		"amount": 1000,
		"checkout_payment": {
			"amount": 1000,
			"billing_address_editable": false,
			"created_at": "2020-05-15T02:00:59Z",
			"customer_editable": false,
			"id": "chk_advD5VdsjJfjlE7k",
			"payment_url": "https://api.mundipagg.com/checkout/v1/orders/chk_advD5VdsjJfjlE7k",
			"shippable": false,
			"skip_checkout_success_page": false,
			"status": "closed",
			"updated_at": "2020-05-15T02:02:27Z"
		},
		"code": "JDOFY4A33Z",
		"created_at": "2020-05-15T02:02:24Z",
		"currency": "BRL",
		"customer": {
			"address": {

				"city": "Rio de Janeiro",
				"complement": "",
				"country": "BR",
				"created_at": "2020-05-15T02:02:24Z",
				"id": "addr_WDXrMyxfbhK6J9jl",
				"neighborhood": "Centro",
				"number": 1213,
				"state": "RJ",
				"status": "active",
				"street": "Rua Guedes Ramos Santos",
				"updated_at": "2020-05-15T02:02:24Z",
				"zip_code": 21467098
			},
			"created_at": "2020-05-07T23:33:15Z",
			"delinquent": false,
			"document": 12345678912,
			"email": "lucia@email.com",
			"id": "cus_WVbg8Qkc0WIelO4k",
			"name": "Lucia Santos",
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
		"id": "ch_2gn67yws0ugEDl3d",
		"last_transaction": {

			"acquirer_auth_code": 197,
			"acquirer_message": "Transação capturada com sucesso",
			"acquirer_name": "stone",
			"acquirer_nsu": 7130,
			"acquirer_return_code": "00",
			"acquirer_tid": 10188458259306,
			"amount": 1000,
			"antifraud_response": {},
			"card": {
				"billing_address": {
					"city": "Rio de Janeiro",
					"complement": "",
					"country": "BR",
					"neighborhood": "Centro",
					"number": 1213,
					"state": "RJ",
					"street": "Rua Guedes Ramos Santos",
					"zip_code": 21467098
				},
				"brand": "visa",
				"created_at": "2020-05-07T23:33:15Z",
				"exp_month": 3,
				"exp_year": 2025,
				"first_six_digits": 400000,
				"holder_document": 12628792729,
				"holder_name": "LUCIA SANTOS",
				"id": "card_XaADo0knUdUDqM32",
				"last_four_digits": "0010",
				"status": "active",
				"type": "credit",
				"updated_at": "2020-05-15T02:02:25Z"

			},
			"created_at": "2020-05-15T02:02:25Z",
			"gateway_id": "84e27b4c-400a-499c-b01b-74fcd159e9aa",
			"gateway_response": {
				"code": 200,
				"errors": []
			},
			"id": "tran_49NMZAPfeINQmPQn",
			"installments": 4,
			"metadata": {},
			"operation_key": 8733852509751,
			"operation_type": "auth_and_capture",
			"status": "captured",
			"success": true,
			"transaction_type": "credit_card",
			"updated_at": "2020-05-15T02:02:25Z"
		},
		"paid_amount": 1000,
		"paid_at": "2020-05-15T02:02:26Z",
		"payment_method": "credit_card",
		"status": "paid",
		"updated_at": "2020-05-15T02:02:26Z"
	}],
	"checkouts": [{
		"accepted_multi_payment_methods": [],
		"accepted_payment_methods": [
			"credit_card"
		],
		"amount": 1000,

		"billing_address": {},
		"billing_address_editable": true,
		"closed_at": "2020-05-15T02:02:27Z",
		"created_at": "2020-05-15T02:00:59Z",
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
			"created_at": "2020-05-15T02:00:58Z",
			"delinquent": false,
			"id": "cus_vXgl4jbjH5im4mbj",
			"name": "Lucia",
			"phones": {},
			"updated_at": "2020-05-15T02:00:58Z"
		},
		"customer_editable": true,
		"expires_at": "2020-05-16T02:00:59Z",
		"id": "chk_advD5VdsjJfjlE7k",
		"metadata": {},
		"payment_url": "https://api.mundipagg.com/checkout/v1/orders/chk_advD5VdsjJfjlE7k",
		"shippable": false,
		"skip_checkout_success_page": true,
		"status": "closed",
		"success_url": "https://sandbox-link.openbank.stone.com.br/t/sucesso",
		"updated_at": "2020-05-15T02:02:27Z"
	}],
	"closed": true,
	"closed_at": "2020-05-15T02:02:27Z",
	"code": "JDOFY4A33Z",
	"created_at": "2020-05-15T02:00:58Z",
	"currency": "BRL",
	"customer": {
		"created_at": "2020-05-15T02:00:58Z",
		"delinquent": false,
		"id": "cus_vXgl4jbjH5im4mbj",
		"name": "Lucia",
		"phones": {},

		"updated_at": "2020-05-15T02:00:58Z"
	},
	"id": "or_ob546qyfOtw6RZnr",
	"items": [{
		"amount": 1000,
		"created_at": "2020-05-15T02:00:58Z",
		"description": "Camisa de malha 100% algodão - Tamanho G - Verde",
		"id": "oi_nkZBpLnH5SkmB8wY",
		"quantity": 1,
		"status": "active",
		"type": "product",
		"updated_at": "2020-05-15T02:00:58Z"
	}],
	"status": "paid",
	"updated_at": "2020-05-15T02:02:28Z"
}
```