---
title: "Criar QRCode Estático"
linkTitle: "Criar QRCode Estático"
date: 2021-08-04T15:19:30-03:00
lastmod: 2021-08-04T15:19:30-03:00
draft: false
weight: 3
description: >
  
---
<br>
Através desse endpoint será possível criar um QRCode Pix estático.
<br>
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_static_invoices
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

**transaction_id*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"

**account_id** `string`

**additional_information** `string`

**amount** `integer`

**key*** `string`


<br>

##### **Response**
---

```
201 OK
```

```json
{
  "id": "<uuid>",
  "account_id": "<uuid>",
  "participant_ispb": "<string>",
  "key": "<string>",
  "key_type": "<string>",
  "transaction_id": "<string>",
  "amount": "<integer>",
  "additional_information": "<string>",  
  "request_id": "<string>",
  "created_at": "<iso8631>",
  "updated_at": "<iso8631>",
  "created_by": "<string>",
  "last_updated_by": "<string>",
  "qr_code_content": "<string>",
  "qr_code_image": "<string>"
}
```

