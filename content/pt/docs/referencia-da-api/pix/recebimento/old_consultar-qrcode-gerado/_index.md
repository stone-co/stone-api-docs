---
title: "Old_Detalhe da Cobrança"
linkTitle: "Old_Detalhe da Cobrança"
date: 2020-11-06T15:26:32-03:00
lastmod: 2020-11-06T15:26:32-03:00
weight: 3
draft: true
description: >
  
---

##### **Request**
```http request
GET /api/v1/pix_payment_invoices/:id
```

##### **Response**
```text
200 OK

{
   "id": "54071fc2-8068-4b26-bed7-be112228ed98",
   "account_id": "fa7da52c-784d-4bd1-a3cb-db98bda9222d",
   "request_id": "f209b07f-f5c4-4a31-b1b8-0d4697ccc92d",
   "key": "571650fa-ae2c-421e-9dfd-c64e0c0c2926",
   "key_type": "random_key",
   "transaction_id": "127a19f8-88d7-4af8-a0b9-1a72f108a40e",
   "amount": 1000,
   "request_for_payer": "Preencha o tamanho da camisa",
   "expiration": 86400,
   "created_at": "2020-08-19T13:49:43Z",
   "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98",
   "paid_at": "2020-08-19T13:49:43Z",
   "cancelled_at": null,
   "updated_at": "2020-08-19T13:49:43Z",
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