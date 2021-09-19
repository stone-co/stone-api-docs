---
title: "Atualizar QRCode Estático"
linkTitle: "Atualizar QRCode Estático"
date: 2021-08-04T15:19:30-03:00
lastmod: 2021-09-19T09:05:30-03:00
draft: false
weight: 4
description: >
  
---
<br>
Através desse endpoint será possível adicionar informações no QRCode estático criado.
<br>
<br>

```
PATCH https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_static_invoices/{{id}}
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-idempotency-key*** `string`
<br> Chave de idempotência.

<br>

##### **PATCH PARAMS**

**id** `uuid`
<br> Identificador do QRCode criado

##### **BODY PARAMS**
---
<br>

**additional_information** `string`

<br>

##### **Response**
---

```
200 OK
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
  "created_at": "<datetime_iso8601>",
  "updated_at": "<datetime_iso8601>",
  "created_by": "<string>",
  "last_updated_by": "<string>",
  "qr_code_content": "<string>",
  "qr_code_image": "<string>"
}
```

