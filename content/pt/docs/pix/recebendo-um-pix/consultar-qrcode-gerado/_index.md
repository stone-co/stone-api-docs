---
title: "Consultar QR Code Gerado"
linkTitle: "Consultar QR Code Gerado"
date: 2020-11-06T15:26:32-03:00
lastmod: 2020-11-06T15:26:32-03:00
weight: 1
description: >
  
---

##### **Request**
Para consultar um único QR Code gerado
```http request
GET - /api/v1/pix_payment_invoices/:id
```

Para consultar vários QR Codes gerados usando diversos filtros
```http request
GET - /api/v1/pix_payment_invoices?filter={
  beneficiary_random_key: string(), 
  created_at: datetime(), 
  beneficiary_type: string(), 
  account_id: uuid(),
  jti: string()
}
```

##### **Headers**
```text
authorization: subject application:participante
content-type: application/json
```

##### **Response**
Resposta de um único QR Code consultado
```text
200 OK

{
   "id": "54071fc2-8068-4b26-bed7-be112228ed98",
   "amount": 1000,
   "created_at": "2020-08-19T13:49:43.094436Z",
   "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98"
   "revision": 0,
   "data_url": "https://api.openbank.stone.com.br/pix/{{jti()}}" 
}
```

Resposta de vários QR Codes consultados
```text
200 OK

{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 25
    },
    "data": [
        {
            "id": "54071fc2-8068-4b26-bed7-be112228ed98",
            "amount": 1000,
            "created_at": "2020-08-19T13:49:43.094486Z",
            "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98"
            "revision": 0,
            "data_url": "https://api.openbank.stone.com.br/pix/{{jti()}}" 
        },
        {
            "id": "54071fc2-8068-4b26-bed7-be112228ed98",
            "amount": 2000,
            "created_at": "2020-08-20T16:19:23.034634Z",
            "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98"
            "revision": 0,
            "data_url": "https://api.openbank.stone.com.br/pix/{{jti()}}" 
        },
        {
            "id": "54071fc2-8068-4b26-bed7-be112228ed98",
            "amount": 3000,
            "created_at": "2020-08-21T20:15:10.014431Z",
            "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98"
            "revision": 0,
            "data_url": "https://api.openbank.stone.com.br/pix/{{jti()}}" 
        }
    ]
}
```
