---
title: "Emitir Boleto"
slug: "emitir-boleto"
draft: false
weight: 5
date: "2020-01-16T19:14:55.374Z"
lastmod: "2021-10-14T10:07:32.971Z"
---

---

<br>

{{< alert title="Horário de funcionamento" >}}

<br>

- **API de Boletos**
  
  Fica disponível para emissão todos os dias da semana, 24 horas por dia;
  
  O registro de boletos é automático, executado no momento da criação do boleto, pode demorar de 3 segundos a 15 minutos a depender do volume de boletos emitidos.

<br>

- **Liquidação de Boletos**
  
Boletos emitidos e pagos na Stone terão a sua liquidação efetuada no mesmo dia. Já boletos emitidos na Stone e pagos em outras instituições, serão liquidados pela <a href="https://www.cip-bancos.org.br/SitePages/Home.aspx" target="_blank">CIP (Câmara Interbancária de Pagamentos)</a> em até D+2 dias úteis e o crédito na conta do cliente ocorrerá no mesmo dia do recebimento da liquidação.

<br>

{{< /alert >}}

<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoices
```
<br>

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
<br>Data limite para pagamento do boleto bancário. Deve ser igual à data de vencimento para boletos de depósito e proposta. Para boletos de cobrança, deve ser maior que a data de vencimento. Se não informada, será usada a expiration_date, nos boletos de depósito e de proposta. Os boletos que forem pagos após a data limite serão devolvidos.

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
<br> &nbsp;&nbsp;&nbsp;&nbsp;**document_type** `string` _(opcional)_
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**legal_name** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;É o nome que identifica o pagador para fins legais, administrativos e outros fins oficiais. Não é obrigatório no tipo `deposit`.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**trade_name** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Nome fantasia do pagador. Obrigatório no caso de pagador PJ.

<br> &nbsp;&nbsp;&nbsp;&nbsp;**address** `object` _(opcional)_

<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**city** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cidade do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**country** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;País do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**extra** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Complemento do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**neighborhood** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bairro do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**postal_code** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CEP do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**state** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UF do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**street** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Logradouro do endereço do pagador do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**street_number** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Número do logradouro do endereço do pagador do boleto.
<br>

<br>

---
<br>

**discounts** `array_of_objects`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**date** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Data até a qual o desconto deve ser aplicado. Formato ISO8601 `"YYYY-MM-DD"`. É aceito nos boletos de proposta e de cobrança.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**value** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Valor percentual (%) do desconto que será aplicado ao boleto. O valor deve ser maior que 0.0 e até 90.0. Formato decimal. Ex: "20.0". É aceito nos tipos de proposta e cobrança.

---
<br>

**fine** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**date** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Data que define o dia a partir do qual a multa deve ser aplicada ao boleto. Caso não seja infromada será consiederada a data de validdade. Só é aceito no boleto de cobrança.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**value** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Valor percentual (%) da multa que será aplicada ao boleto. O valor do deve ser maior que 0.0 e até 2.0. Formato decimal. Ex: "2.0". Só é aceito no boleto de cobrança.

---
<br>

**interest** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**date** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Data que define o dia a partir do qual os juros passam a ser aplicados ao boleto. Só é aceito no boleto de cobrança.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**value** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Valor parcentual (%) dos juros que será aplicado ao boleto por mês. O valor do deve ser maior que 0.0 e até 1.0. Formato decimal. Ex: "1.0". Só é aceito no boleto de cobrança.

---
<br>

**receiver** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**legal_name** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;É o nome que identifica o sacado avalista para fins legais, administrativos e outros fins oficiais.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**document** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Número do documento do sacador avalista.

---
<br>

**address** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**city** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Cidade do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**country** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;País do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**extra** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Complemento do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**neighborhood** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Bairro do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**postal_code** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;CEP do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**state** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;UF do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**street** `string` _(obrigatório)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;Logradouro do endereço do beneficiário do boleto.
<br>
<br> &nbsp;&nbsp;&nbsp;&nbsp;**street_number** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Número do logradouro do beneficiário do boleto.
<br>

---
<br>

**payment_invoice** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**description** `string` _(opcional)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;A cliente poderá adicionar informações relativas ao seu produto/serviço a fim de identificar o que foi vendido.
<br>

---
<br>**metadata** `object` _(opcional)_
<br>Preenchido com dados internos do parceiro. 

---
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

#### **Responses**

```json
200 OK
content-type: application/json
```
Body
```json

{
	"account_id": "ec363b21-113f-44e9-8cc3-dfcdb3cc2dc3",
    "amount": 2100,
    "barcode": "19797845600000021000000063139072468215929006",
    "beneficiary": {
      "account_code": "1085737",
      "address": {
        "city": "Rio de Janeiro",
        "country": "Brazil",
        "extra": null,
        "neighborhood": "Centro",
        "postal_code": "20021-290",
        "state": "RJ",
        "street": "Rua do Passeio",
        "street_number": null
      },
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
   "writable_line": "19790000056313907246482159290061784560000002100",
   "payment_invoice": {
     "description": "Descrição do pagamento."
   },
   "metadata": {}
}
```
<br>


```json
201 Created
```
Body
```json
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
  "payer": {
    "document": "11121740790",
    "document_type": "cpf",
    "legal_name": "Pereira da Silva",
    "trade_name": null
  },
  "receiver": null,
  "registered_at": null,
  "settled_at": null,
  "status": "CREATED",
  "writable_line": "19790000056313907246482159290061784560000002100",
  "payment_invoice": {
     "description": "Descrição do pagamento."
  },
  "metadata": {}
}
```
<br>

```json
400 Bad Request
```
Body
```json
{
  "reason": [
    {
      "error": "is invalid",
      "path": [
        "customer",
        "trade_name"
      ]
    },
    {
      "error": "is invalid",
      "path": [
        "customer",
        "legal_name"
      ]
    }
  ],
  "type": "srn:error:validation"
}
```
<br>

```json
401 Unauthorized
```
Body
```json
{
  "type": "srn:error:unauthenticated"
}
```
<br>

```json
403 Forbidden
```
Body
```json
{
  "type": "srn:error:unauthorized"
}
```
<br>

```json
409 Conflict
```
Body
```json
{
  "type": "srn:error:conflict"
}
```
<br>

```json
422 Unprocessable Entity
```
Body
```json
{
  "reason": "barcode_payment_invoice_bill_of_exchange is not ena bled on this account",
  "type": "srn:error:product_not_enabled"
}
```
<br>
