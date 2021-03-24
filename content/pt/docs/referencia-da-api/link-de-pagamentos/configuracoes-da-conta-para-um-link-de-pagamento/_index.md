---
title: "Configurações da Conta para um Link de Pagamento"
linkTitle: "Configurações da conta para um Link de Pagamento"
date: 2021-03-10T15:30:00-03:00
lastmod: 2021-03-11T14:00:00-03:00
weight: 2
description: >
---
---

<br>

Cada Conta Stone possui sua própria configuração de criação de link de pagamento que limitam valor máximo permitido, configurações de checkout e outros parâmetros. 


{{% pageinfo %}}
**Atenção**

É importante que antes da criação de qualquer link de pagamento as configurações da conta sejam checadas.

{{% /pageinfo %}}

---

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/payment_links/{account_id}/config
```

##### Response

```Json
{
	"accepted_multi_payment_methods": [],
	"bank_slip": {
		"bank": 197,
		"enabled": false,
		"expires_in": 2,
		"instructions": "Pagar até o vencimento"
	},
	"billing_address_editable": false,
	"closed": false,
	"credit_card": {
		"capture": true,
		"enabled": true,
		"max_installments": 12
	},
	"customer_editable": true,
	"max_amount": 5000000,
	"min_amount": 100,
	"payment_method": "checkout",
	"payment_url_host": "http: //link.homolog.stone.credit",

	"skip_checkout_success_page": true,
	"success_url": "/sucesso"
}
```