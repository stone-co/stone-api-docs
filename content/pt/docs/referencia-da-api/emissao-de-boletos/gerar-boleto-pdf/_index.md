---
title: "Gerar PDF Boleto"
slug: "gerar-pdf-boleto"
draft: false
weight: 8
date: "2020-09-22T15:54:16.171Z"
lastmod: "2020-09-22T15:54:16.171Z"
---
---

<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/exports/barcode_payment_invoices/id
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

{ }
