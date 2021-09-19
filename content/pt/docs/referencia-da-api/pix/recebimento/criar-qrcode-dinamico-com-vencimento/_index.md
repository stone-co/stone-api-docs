---
title: "Criar QRCode Dinâmico com Validade"
linkTitle: "Criar QRCode Dinâmico com Validade"
slug: "criar-qrcode-dinamico-com-validade"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-09-19T09:02:00-03:00
draft: false
weight: 7
description: >
  
---
<br>
Através desse endpoint será possível criar cobranças Pix com vencimento através de um QRCode ou Pix copia e cola.
<br>
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_invoices_with_due_date
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-idempotency-key*** `string`
<br> Chave de idempotência.

<br>

##### **BODY PARAMS**
---
<br>

**account_id*** `string`
<br>Identificador da conta que irá receber o valor pago.

**additional_data** `object` 

&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tamanho: min 1 / max 50
<br>&nbsp;&nbsp;&nbsp;&nbsp;**value** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tamanho: min 1 / max 200

**amount** `integer`

**customer*** `object` 

&nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`

**discount** `object`

&nbsp;&nbsp;&nbsp;&nbsp;**type** `string` 
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores aceitos: `fixed`, `proportional`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**calculation_mode** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores aceitos: `date`, `period`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**period_discount** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**fixed_value** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Se type:fixed.
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**proportional** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Se type:proportional. Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**coefficient** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**exponent** `integer`

**expiration_date*** `string`
<br>Format: date

**fine** `object`

&nbsp;&nbsp;&nbsp;&nbsp;**type** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores aceitos: `fixed`, `proportional` 
<br>&nbsp;&nbsp;&nbsp;&nbsp;**fixed_value** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Se type:fixed.
<br>&nbsp;&nbsp;&nbsp;&nbsp;**proportional_value** `object` 
<br>&nbsp;&nbsp;&nbsp;&nbsp;Se type:proportional. Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**coefficient** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**exponent** `integer`

**interest** `object`

&nbsp;&nbsp;&nbsp;&nbsp;**type** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores aceitos: `fixed`, `proportional`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**period** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores aceitos: `day`, `month`, `year`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**fixed_value** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Se type:fixed.
<br>&nbsp;&nbsp;&nbsp;&nbsp;**proportional_value** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Se type:proportional. Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**coefficient** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**exponent** `integer`

**key*** `string`

**only_business_days** `boolean`
<br>Aceia true or false para pagamento somente em dias úteis

**payment_limit_period_days** `integer`
<br>Informa por quanto tempo o QRCode estará válido.

**reduction** `object`

&nbsp;&nbsp;&nbsp;&nbsp;**type** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valores aceitos: `fixed`, `proportional` 
<br>&nbsp;&nbsp;&nbsp;&nbsp;**fixed_value** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Se type:fixed.
<br>&nbsp;&nbsp;&nbsp;&nbsp;**proportional_value** `object` 
<br>&nbsp;&nbsp;&nbsp;&nbsp;Se type:proportional. Representação de porcentagem, dada a seguinte fórmula: `coefficient * 10^exponent`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**coefficient** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**exponent** `integer`

**request_for_payer** `string`
<br>Descrição opcional do QRCode.

**transaction_id*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"

<br>
Exemplo:

```json
{
	"account_id": "{{account_id}}",
	"additional_data": [{
		"name": "Título",
		"value": "Descrição"
	}],
	"amount": 15,
	"customer": {
		"document": "14423692724",
		"document_type": "cpf",
		"name": "John Doe"
	},
	"discount": {
		"calculation_mode": "period",
		"period_discount": {
			"fixed_value": 60
		},
		"type": "fixed"
	},
	"expiration_date": "2021-06-15",
	"fine": {
		"fixed_value": 100,
		"type": "fixed"
	},
	"interest": {
		"fixed_value": 50,
		"period": "day",
		"type": "fixed"
	},
	"key": "4e4bb64d-d17c-4c53-a51b-44f06e28be06",
	"only_business_days": false,
	"payment_limit_period_days": 15,
	"reduction": {
		"fixed_value": 100,
		"type": "fixed"
	},
	"request_for_payer": "do something",
	"transaction_id": "2b99dae0492c425c969e7768a91b2f3d"
}
```

<br>

##### **Response**
---

```
200 OK
```

```json
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "additional_data": [
    {
      "name": "Mr. Due",
      "value": "Date"
    }
  ],
  "amount": 555,
  "beneficiary_address": {
    "city": "Rio de JaneiroA",
    "country": "BRA",
    "extra": "A",
    "neighborhood": "FlamengoA",
    "postal_code": "22250120",
    "reference_point": null,
    "state": "RJA",
    "street": "Rua Honório de BarrosoA",
    "street_number": "3A"
  },
  "beneficiary_entity": {
    "document": "91092573062",
    "document_type": "cpf",
    "legal_name": "Gilderoy Lockhart",
    "trade_name": null
  },
  "cancelled_at": null,
  "created_at": "2021-03-19T14:43:55Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "customer": {
    "document": "85553990335",
    "document_type": "cpf",
    "name": "Fulano da Silva"
  },
  "discount": null,
  "expiration_date": "2021-03-19",
  "fine": null,
  "id": "b4bdc3df-795e-4d33-9851-15192fb7e216",
  "inbound_pix_payments": [],
  "interest": null,
  "key": "4e4bb64d-d17c-4c53-a51b-44f06e28be06",
  "key_type": "random_key",
  "location": "pix-h.stone.com.br/pix/v2/cobv/b4bdc3df-795e-4d33-9851-15192fb7e216",
  "only_business_days": false,
  "paid_at": null,
  "payment_limit_period_days": 30,
  "qr_code_content": "00020101021226890014br.gov.bcb.pix2567pix-h.stone.com.br/pix/v2/cobv/b4bdc3df-795e-4d33-9851-15192fb7e21652040000530398654045.555802BR5925Nome do CPF 581.360.533-96014RIO DE JANEIRO622905253f6a429254c34b3091847f85d63046EBC",
  "qr_code_image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfgAAAH4CAIAAAApSmgoAAA590lEQVR4nO2bMaIjSbIj//0vvauMGvWIpFnDPRlQyxswIB5Tmvm//3d1dXV19Wr9Xxvg6urq6srV/dBfXV1dvVz3Q391dXX1ct0P/dXV1dXLdT/0V1dXVy/X/dBfXV1dvVz3Q391dXX1ch0/9P+3RCk/dW/vluZSPHYvKpfawfb5dpennFSvaTyUT+qf+rR05H9tMfne3i3NpXjsXlQutYPt8+0uTzmpXtN4KJ/UP/Vp6cj/2mLyvb1bmkvx2L2oXGoH2+fbXZ5yUr2m8VA+qX/q09KR/7XF5Ht7tzSX4rF7UbnUDrbPt7s85aR6TeOhfFL/1KelI/9ri8n39m5pLsVj96JyqR1sn293ecpJ9ZrGQ/mk/qlPS0f+1xaT7+3d0lyKx+5F5VI72D7f7vKUk+o1jYfySf1Tn5aO/K8tJt/bu6W5FI/di8qldrB9vt3lKSfVaxoP5ZP6pz4tHflfW0y+t3dLcykeuxeVS+1g+3y7y1NOqtc0Hson9U99Wjry20NTiotRAw0Ttc",
  "reduction": null,
  "request_for_payer": "do something until today",
  "request_id": "f06fe0c17b96d26965b069c73b77153c",
  "status": "ACTIVE",
  "transaction_id": "3f6a429254c34b3091847f85da88eb65",
  "updated_at": "2021-03-19T14:43:55Z"
}
```

---

```
400 Bad Request
```

```json
{
  "reason": [
    {
      "error": "is invalid",
      "path": [
        "key_type"
      ]
    },
    {
      "error": "is invalid",
      "path": [
        "status"
      ]
    }
  ],
  "type": "srn:error:validation"
}
```

---

```
401 Unauthorized
```

```json
{
  "type": "srn:error:unauthorized"
}
```

---

```
403 Forbidden
```

```json
{
  "type": "srn:error:unauthenticated"
}
```

---

```
409 Conflict
```

```json
{
  "type": "srn:error:idempotency_conflict"
}
```

---

```
422 Unprocessable
```

```json
{
  "reason": [
    {
      "error": "has already been taken",
      "path": [
        "transaction_id"
      ]
    }
  ],
  "type": "srn:error:unprocessable_entity"
}
```
