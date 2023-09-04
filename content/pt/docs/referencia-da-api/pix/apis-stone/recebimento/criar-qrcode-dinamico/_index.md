---
title: "Criar QRCode Dinâmico"
linkTitle: "Criar QRCode Dinâmico"
date: 2021-09-19T08:55:30-03:00
lastmod: 2021-09-19T08:55:30-03:00
slug: "criar-qr-code-dinamico"
draft: false
weight: 6
description: >
  
---
<br>
Através desse endpoint será possível criar um QRCode Pix dinâmico imediato.
<br>
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix_payment_invoices
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

**amount** `integer`

**account_id*** `string`

**key*** `string`

**transaction_id*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"

**customer** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;**document** `string`

**additional_data** `object` 

&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tamanho: min 1 / max 50
<br>&nbsp;&nbsp;&nbsp;&nbsp;**value** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tamanho: min 1 / max 200

**metadata** `object` 

&nbsp;&nbsp;&nbsp;&nbsp;**name** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tamanho: min 1 / max 50
<br>&nbsp;&nbsp;&nbsp;&nbsp;**value** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tamanho: min 1 / max 200

**expiration** `integer`
<br>Tempo de expiração. O valor padrão é de 24h caso não seja enviado

**request_for_payer** `string`
<br>Descrição opcional do QRCode.

<br>

Exemplo:

```json
{
    "amount":"100",
    "account_id":"7e785e98-c859-46c6-9dc7-37ea522ceadf",
    "key":"92961229022",
    "transaction_id":"1234567898745236521478edrfth4r",
    "customer": {
        "name": "Maria",
        "document": "12409265606"
    },
    "request_for_payer":"Pague"
}
```

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
  "additional_data": "<object>",  
  "metadata": "<object>",
  "location": "<string>",
  "request_for_payer": "<string>",
  "expiration": "<integer>",
  "status": "<string>",
  "request_id": "<string>",
  "created_at": "<datetime_iso8601>",
  "paid_at": "<datetime_iso8601>",
  "cancelled_at": "<datetime_iso8601>",
  "updated_at": "<datetime_iso8601>",
  "created_by": "<string>",
  "last_updated_by": "<string>",
  "qr_code_content": "<string>",
  "qr_code_image": "<string>"
}
```

```
400 Bad Request
```

```json
{
  "reason": [
    {
      "error": "is invalid",
      "path": [
        "amount"
      ]
    },
    {
      "error": "is invalid",
      "path": [
        "status"
      ]
    }
  ],
  "type": "srn:error:validation"
}
```

---

```
401 Unauthorized
```

```json
{
  "type": "srn:error:unauthenticated"
}
```
---

```
403 Forbidden
```

```json
{
  "type": "srn:error:unauthorized"
}
```
