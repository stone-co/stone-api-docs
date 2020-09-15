---
title: "Receber um PIX via QR Code"
date: 2020-09-14T18:15:48-03:00
lastmod: 2020-09-14T18:15:48-03:00
weight: "3"
draft: false
---

Para receber um PIX via QR Code, a cliente precisa ter a sua chave aleatória cadastrada na instituição participante.

#### Criação de um QR Code

##### Exemplo de requisição:
```textmate
POST /api/v1/pix_payment_invoices
authorization: subject application:participante
content-type: application/json
x-stone-idempotency-key: string()

{
  "amount": integer(),
  "expiration": integer() | null, # valor em segundos, campo é opcional!
  "account_id": uuid() # ID da conta da participante,
  "customer_type": "stone_account" | "external_account",
  "customer_random_key": <dict_key> | null # do cliente da participante e precisa ser a chave dinâmica. Caso seja nula, assumimos que é a random do cliente
}

 - inside-gateway -> pix-dispatcher
 - pix-dispatcher autoriza a criação
   - action: create_pix_invoice_participant_public
   - resource: paymentaccount/{{account_id()}}
   - scope: paymentaccount:pix_invoice
   - application_config: flag indirect_participant == true
```

##### Exemplo de resposta:
```textmate
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

#### Consulta de um QR code gerado:

##### Exemplo de requisição:
```textmate
GET /api/v1/pix_payment_invoices/:id
authorization: subject application:participante
content-type: application/json
```
##### Exemplo de resposta:
```textmate
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
##### Exemplo de requisição de uma lista paginada:
```textmate
GET /api/v1/pix_payment_invoices?filter={
  customer_random_key: string(), 
  created_at: datetime(), 
  customer_type: string(), 
  account_id: uuid(),
  jti: string()
}
authorization: subject application:participante
content-type: application/json
```

##### Exemplo de resposta:
```textmate
200 OK

{{ lista paginada de resultados }}
```

#### Leitura de um QR Code gerado:
(em breve)