---
title: "Emitir Boleto"
slug: "emitir-boleto"
draft: false
weight: 5
date: "2020-01-16T19:14:55.374Z"
lastmod: "2020-12-21T20:31:32.971Z"
---

---
```http request
POST https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoices
```
---

#### **BODY PARAMS**
---
<br>

**account_id*** `string`
<br> Identificador da conta que irá gerar o documento.

---
<br>

**amount*** `int32`
<br> Valor do boleto em centavos de Real, ou seja, 20 reais fica 2000.

---
<br>

**expiration_date*** `string`
<bR>Data de vencimento do boleto bancário. Mesmo depois dessa data expirar o pagamento ainda pode ser feito. Formato: `yyyy-mm-dd`

---
<br>

**limit_date** `string`
<br>Data limite para pagamento do boleto bancário. Deve ser igual ou maior que data de vencimento. Se não informada, será usada a `expiration_date`.

---
<br>

**invoice_type*** `string`
<br>Tipo de boleto bancário. Valores suportados: `proposal`, `deposit` e `bill_of_exchange`.

---
<br>

**customer** `object`
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**document** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Número do documento do pagador sem pontos. Não é obrigatório no tipo `deposit`.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**legal_name** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais. Não é obrigatório no tipo `deposit`.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**trade_name** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Nome fantasia do pagador. Obrigatório no caso de pagador PJ.

---
<br>

**discounts** `array_of_objects`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**date** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Data até a qual o desconto deve ser aplicado. Formato ISO8601 `"YYYY-MM-DD"`. Só é aceito no tipo de cobrança.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**value** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Valor percentual (%) do desconto que será aplicado ao boleto. O valor do deve ser maior que 0.0 e até 90.0. Formato decimal. Ex: "20.0". Só é aceito no tipo de cobrança.

---
<br>

**fine** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**date** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Data que define o dia a partir do qual a multa deve ser aplicada ao boleto. Caso não seja infromada será consiederada a data de validdade. Só é aceito no tipo de cobrança.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**value** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Valor percentual (%) da multa que será aplicada ao boleto. O valor do deve ser maior que 0.0 e até 2.0. Formato decimal. Ex: "2.0". Só é aceito no tipo de cobrança.

---
<br>

**interest** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**date** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Data que define o dia a partir do qual os juros passam a ser aplicados ao boleto. Só é aceito no tipo de cobrança.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**value** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Valor parcentual (%) dos juros que será aplicado ao boleto por mês. O valor do deve ser maior que 0.0 e até 1.0. Formato decimal. Ex: "1.0". Só é aceito no tipo de cobrança.

---
<br>

**receiver** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**legal_name** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;É o nome que identifica o sacado avalista para fins legais, administrativos e outros fins oficiais.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Número do documento do sacador avalista.


<br><br>



#### **HEADERS**
---
<br>

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

<br>

{{% pageinfo %}}
**Data limite no tipo `proposal`**
<br>A `limit_date` será sempre igual a `expiration_date` para boletos do tipo `proposal` uma vez que a proposta é válida somente até a data do vencimento.
{{% /pageinfo %}}

<br>

#### **Response**

```JSON
200 OK
content-type: application/json
```
Body
```JSON

{
	"account_id": "ec363b21-113f-44e9-8cc3-dfcdb3cc2dc3",
    "amount": 2100,
    "barcode": "19797845600000021000000063139072468215929006",
    "beneficiary": {
      "account_code": "1085737",
      "branch_code": "1",
      "document": "39809096038",
      "document_type": "cpf",
      "legal_name": "Pereira da Silva",
      "trade_name": null
    },
    "created_at": "2020-07-27T18:25:38Z",
    "created_by": "user:34a071d5-e1d4-4cb0-acf7-ca9b106fec65",
    "customer": {
      "document": "11121744590",
      "document_type": "cpf",
      "legal_name": "Pereira da Silva",
      "trade_name": null
    },
    "discounts": [
      {
        "date": "2020-11-20",
        "value": "0.1"
      }
    ],
    "expiration_date": "2020-12-01",
    "fee": 0,
    "fee_metadata": {
      "billing_exemption_participant": true,
      "fee": 0,
      "max_free": 5,
      "original_fee": 200,
      "remaining_free": 5
    },
    "fine": {
      "date": "2021-01-02",
      "value": "1"
    },
    "id": "172caf21-13de-4baa-9823-a21ac17ba8fa",
    "interest": {
      "date": "2021-01-02",
      "value": "1"
    },
    "invoice_type": "bill_of_exchange",
    "issuance_date": "2020-07-27",
    "limit_date": "2021-02-01",
    "our_number": "63139072468215929006",
    "customer": {
      "document": "11121740790",
      "document_type": "cpf",
      "legal_name": "Pereira da Silva",
      "trade_name": null
    },
   "receiver": null,
   "registered_at": null,
   "settled_at": null,
    "status": "CREATED",
    "writable_line": "19790000056313907246482159290061784560000002100"
}
