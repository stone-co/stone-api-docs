---
title: "Detalhar QRCode Estático"
linkTitle: "Detalhar QRCode Estático"
date: 2021-08-04T15:19:30-03:00
lastmod: 2021-08-04T15:19:30-03:00
draft: false
weight: 5
description: >
  
---
<br>
Através desse endpoint será possível detalhar um QRCode estático criado.
<br>
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_static_invoices/{{id}}
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-idempotency-key*** `string`
<br> Chave de idempotência.

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
  "created_at": "<iso8631>",
  "updated_at": "<iso8631>",
  "created_by": "<string>",
  "last_updated_by": "<string>",
  "qr_code_content": "<string>",
  "qr_code_image": "<string>"
}
```

---
