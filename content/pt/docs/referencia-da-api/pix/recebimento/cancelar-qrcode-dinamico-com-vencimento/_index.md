---
title: "Cancelar QRCode Dinâmico com data de vencimento"
linkTitle: "Cancelar QRCode Dinâmico com data de vencimento"
date: 2022-02-18T14:00:00-03:00
lastmod: 2022-02-18T14:08:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível cancelar as cobranças por Pix com data de vencimento.

```
DELETE https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_invoices_with_due_date/{{id}}
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **PATH PARAMS**

**id** `uuid`
<br> Identificador do QRCode com data de vencimento

<br>

##### **Response**
---

```
204 OK
```
