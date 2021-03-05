---
title: "Inserindo Dados Completos"
linkTitle: "Inserindo Dados Completos"
date: 2020-11-06T12:31:11-03:00
lastmod: 2020-11-06T12:31:11-03:00
weight: 1
draft: true
description: >
  
---

Essa forma de pagamento se assemelha muito com uma TED. É preciso saber os seguintes dados do recebedor:
- Instituição (ispb)
- Nome
- Documento (CPF ou CNPJ)
- Agência
- Conta
- Tipo de Conta (corrente, poupança, de pagamento etc)

<br>

##### **Request**

```http request
POST /api/v1/pix_payments
```

##### **Headers**
```text
"authorization": subject application:participante
"content-type": application/json
```

##### **Body**
```text
{
  "tx_id": "0899c742038a4c00bf4c63260c61dbff",
  "amount": 1000,
  "description": "teste",
  "source_name": "Bacen",
  "source_document": "11111111111",
  "source_account_code": "1",
  "source_account_type": "CACC",
  "source_branch": "1",
  "source_ispb": "99999003",
  "target_name": "Vitor",
  "target_document": "62183746025",
  "target_account_code": "3643277",
  "target_account_type": "CACC",
  "target_branch": "0001",
  "target_ispb": "16501555"
}
```

##### **Response**

```text
201 CREATED

{
  "tx_id": "0899c742038a4c00bf4c63260c61dbff",
  "created_at": "2020-08-19T13:49:43.094436Z",
  "created_by": "user:54071fc2-8068-4b26-bed7-be112228ed98",
  "amount": 1000,
  "description": "teste",
  "source_name": "Bacen",
  "source_document": "11111111111",
  "source_account_code": "1",
  "source_account_type": "CACC",
  "source_branch": "1",
  "source_ispb": "99999003",
  "target_name": "Vitor",
  "target_document": "62183746025",
  "target_account_code": "3643277",
  "target_account_type": "CACC",
  "target_branch": "0001",
  "target_ispb": "16501555"
}
```