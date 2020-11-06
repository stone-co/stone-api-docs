---
title: "Gerar Cobrança com QR Code dinâmico"
linkTitle: "Gerar Cobrança com QR Code dinâmico"
date: 2020-11-06T13:55:15-03:00
lastmod: 2020-11-06T13:55:15-03:00
weight: 1
description: >
  
---

##### **Request**
```http request
POST - /api/v1/pix_payment_invoices
```

##### **Headers**
```text
"authorization": subject application:participante
"content-type": application/json
"x-stone-idempotency-key": string
```

##### **Body**
```text
{
  "account_id": uuid() # ID da conta da participante,
  "key": <string>, # chave do dict
  "transaction_id": <string>, # pattern: [A-Z0-9-]{1,35}
  "amount": integer(), # min 1, max 999_999_999_999
  "request_for_payer": string() | null, # 140 caracteres no max
  "expiration": integer() | null, # valor em segundos, default 86400
  "customer": {
    "name": string(), # min 1 caracter, max 200 caracteres. Nome do pagador cadastrado na geração da cobrança (não necessariamente é o pagador final)
    "document": string() # min 1 caracter, max 200 caracteres. Documento do pagador cadastrado na cobrança
  } | null,
  additional_data: [ # máximo de 50 itens na lista, mínimo de 1 ou nulo
    {
      "name": string(), # min 1 caractere, max 50 caracteres
      "value": string() # min 1 caractere, max 200 caracteres
    }
  ] | null
}
```

##### **Response**
```text
201 CREATED

{
   "id": "54071fc2-8068-4b26-bed7-be112228ed98",
   "account_id": "fa7da52c-784d-4bd1-a3cb-db98bda9222d",
   "request_id": "f209b07f-f5c4-4a31-b1b8-0d4697ccc92d",
   "key": "571650fa-ae2c-421e-9dfd-c64e0c0c2926",
   "transaction_id": "127a19f8-88d7-4af8-a0b9-1a72f108a40e",
   "amount": 1000,
   "request_for_payer": "Preencha o tamanho da camisa",
   "expiration": 86400,
   "created_at": "2020-08-19T13:49:43Z",
   "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98"
   "revision": 0,
   "location": "pix.stone.com.br/pix/1dd7f893-a58e-4172-8702-8dc33e21a403",
   "status": "ACTIVE",
   "customer": {
     "name": "Fulano da Silva"
     "document": "18894559890"
   },
   "additional_data": [
    {
      "name": "Modelo",
      "value": "Camisa Kelvin Clain Luxo"
    },
    {
      "name": "Cor",
      "value": "Dourada"
    }
  ]
}
```