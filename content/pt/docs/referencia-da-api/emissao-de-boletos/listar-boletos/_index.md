---
title: "Listar Boletos"
slug: "listar-boletos"
draft: false
weight: 6
date: "2020-03-09T17:11:01.543Z"
lastmod: "2020-03-09T17:11:01.543Z"
---
---

<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoices
```
<br>

#### **QUERY PARAMS**
---
<br>

**account_id*** `string`
<br> Identificador da conta.

---
<br>

**before** `string`
<br> Cursor opaco da paginação.

---
<br>

**after** `string`
<br> Cursor opaco da paginação.

---
<br>

**limit** `integer`
<br> Limite de itens retornados.

---
<br>

**invoice_type** `string`
<br> Valores permitidos: deposit, proposal ou bill_of_exchange.

---
<br>

**status** `string`
<br> Valores Permitidos: CREATED, SETTLED, REGISTERED, CANCELLED, EXPIRED, PENDING.

---
<br>

**amount** `integer`
<br> Valor do boleto bancário gerado, em centavos de reais.

---
<br>

**issuance_date** `string`
<br> Data da emissão de boleto bancário. Formato "YYYY-MM-DD".

---
<br>

**expiration_date** `string`
<br> Data de vencimento do boleto bancário. Mesmo depois dessa data expirar o pagamento ainda pode ser feito.
Formato "YYYY-MM-DD". 

---
<br>

**settled_date** `string`
<br> Data de liquidação do boleto.

---
<br>

**amount_lt** `integer`
<br> Valor menor que

---
<br>

**amount_gt** `integer`
<br> Valor maior que

---
<br>

**start_limit_date** `string`
<br> Listar boletos com data limite a partir dessa data

---
<br>

**end_limit_date** `string`
<br> Listar boletos com data limite até essa data

---
<br>

**start_expiration_date** `string`
<br> Listar boletos com data de vencimento a partir dessa data

---
<br>

**end_expiration_date** `string`
<br> Listar boletos com data de vencimento até essa data

---
<br>

**start_issuance_date** `string`
<br> Listar boletos com data de emissão a partir dessa data 

---
<br>

**end_issuance_date** `string`
<br> Listar boletos com data de emissão até essa data

---
<br>

**start_settled_date** `string`
<br> Listar boletos com data de liquidação a partir dessa data

---
<br>

**end_settled_date** `string`
<br> Listar boletos com data de liquidação até essa data

---
<br>

**barcode**`string`
<br> Código de barras.

---
<br>

**writable_line**`string`
<br> Código de barras traduzidos em números.

---
<br>

**payment_invoice** `object`
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**description** `string` _(opcional)_
<br> &nbsp;&nbsp;&nbsp;&nbsp;A cliente poderá adicionar informações relativas ao seu produto/serviço a fim de identificar o que foi vendido.

<br><br>

#### **Response**

```
200 OK
content-type: application/json
```

##### Body

```json

{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 25
    },
    "data": [
       {
          "account_id":"8cbeb3d2-750f-4b14-81a1-143ad715c273",
          "amount":2000,
          "barcode":"19795819100000020000000020200310150334476155",
          "beneficiary":{
             "account_code":"498910",
             "branch_code":"1",
             "document":"98146856000174",
             "document_type":"cnpj",
             "legal_name":"Sr. Mirella",
             "trade_name":null
          },
          "created_at":"2020-03-10T15:03:34Z",
          "created_by":"user:380f9969-8946-4f88-a781-be8b7efc1f90",
          "customer": {
             "document": "11121740755",
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
          "expiration_date":"2020-03-11",
          "fee":0,
          "fine": {
             "date": "2021-01-02",
             "value": "1"
          },
          "id":"2788e49f-6f53-4296-bba4-3eb5101ff3e8",
          "interest": {
             "date": "2021-01-02",
             "value": "1"
          },
          "invoice_type":"proposal",
          "issuance_date":"2020-03-10",
          "limit_date":"2020-03-11",
          "our_number": "20200427112605941833",
          "customer":{
             "document":"98146856000174",
             "document_type":"cnpj",
             "legal_name":"Sr. Mirella",
             "trade_name":null
          },
          "receiver": null,
          "registered_at":"2020-03-10T15:03:34Z",
          "settled_at":null,
          "status":"REGISTERED",
          "writable_line":"19790000052020031015703344761550581910000002000"
       },
       {
          "account_id":"8cbeb3d2-750f-4b14-81a1-143ad715c273",
          "amount":2000,
          "barcode":"19795819100000020000000020200310150334476155",
          "beneficiary":{
             "account_code":"498910",
             "branch_code":"1",
             "document":"98146856000174",
             "document_type":"cnpj",
             "legal_name":"Sr. Mirella",
             "trade_name":null
          },
          "created_at":"2020-03-10T15:03:34Z",
          "created_by":"user:380f9969-8946-4f88-a781-be8b7efc1f90",
          "customer": {
             "document": "11121740755",
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
          "expiration_date":"2020-03-11",
          "fee":0,
          "fine": {
             "date": "2021-01-02",
             "value": "1"
          },
          "id":"2788e49f-6f53-4296-bba4-3eb5101ff3e8",
          "interest": {
             "date": "2021-01-02",
             "value": "1"
          },
          "invoice_type":"proposal",
          "issuance_date":"2020-03-10",
          "limit_date":"2020-03-11",
          "our_number": "20200427112605941833",
          "customer":{
             "document":"98146856000174",
             "document_type":"cnpj",
             "legal_name":"Sr. Mirella",
             "trade_name":null
          },
          "receiver": null,
          "registered_at":"2020-03-10T15:03:34Z",
          "settled_at":null,
          "status":"REGISTERED",
          "writable_line":"19790000052020031015703344761550581910000002000",
          "payment_invoice": {
            "description": "Descrição do pagamento."
          }
 
       }
    ]
}
```
<br>

```
403 Forbidden
```

##### Body

```json
{
  "type": "object",
  "properties": {
    "type": {
      "type": "string",
      "enum": [
        "srn:error:unauthorized"
      ]
    }
  }
}
```
