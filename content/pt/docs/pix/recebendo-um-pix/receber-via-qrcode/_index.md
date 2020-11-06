---
title: "Receber via QR Code"
linkTitle: "Receber via QR Code"
date: 2020-11-06T15:21:35-03:00
lastmod: 2020-11-06T15:21:35-03:00
weight: 1
description: >
  
---

Para receber um PIX via QR Code, a cliente precisa ter a sua chave aleatória cadastrada na instituição participante.

##### **Request**
```http request
POST - /api/v1/pix_payment_invoices
```

##### **Headers**
```text
authorization: subject application:participante
content-type: application/json
x-stone-idempotency-key: string
```

##### **Body**
```text
{
  "amount": integer(),
  "expiration": integer() | null, # valor em segundos, campo é opcional!
  "account_id": uuid() # ID da conta da participante,
  "beneficiary_type": "stone_account" | "external_account",
  "beneficiary_random_key": <dict_key> | null # do cliente da participante e precisa ser a chave dinâmica. Caso seja nula, assumimos que é a random do cliente
}
```

##### **Response**
```text
201 CREATED

{
   "id": "54071fc2-8068-4b26-bed7-be112228ed98",
   "amount": 1000,
   "created_at": "2020-08-19T13:49:43.094436Z",
   "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98"
   "revision": 0,
   "data_url": "https://api.openbank.stone.com.br/pix/{{jti()}}"
}
```