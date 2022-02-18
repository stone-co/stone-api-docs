---
title: "Cancelar QRCode Dinâmico"
linkTitle: "Cancelar QRCode Dinâmico"
date: 2022-02-18T14:00:00-03:00
lastmod: 2022-02-18T14:08:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível cancelar as cobranças por Pix.

```
DELETE https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_invoices/{{id}}
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
<br> Identificador do QRCode criado


<br>

##### **Response**
---

```
204 OK
```
