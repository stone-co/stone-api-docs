---
title: "Retornar Um Boleto"
slug: "retornar-um-boleto"
draft: false
weight: 7
date: "2020-03-06T17:19:19.691Z"
lastmod: "2020-03-06T17:19:19.691Z"
---
---

<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoices/id
```
<br>

#### **PATH PARAMS**
---
<br>

**id*** `string`
<br> Identificador do boleto.

<br>

#### **Response**

```json
200 OK
content-type: application/json
```
Body
```json

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
             "trade_name":NULL
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
             "trade_name":NULL
          },
          "receiver": null,
          "registered_at":"2020-03-10T15:03:34Z",
          "settled_at":NULL,
          "status":"REGISTERED",
          "writable_line":"19790000052020031015703344761550581910000002000",
          "payment_invoice": {
            "description": "Descrição do pagamento."
          },
          "metadata": {}
 }
