---
title: "Pagar um PIX"
date: 2020-09-14T18:16:35-03:00
lastmod: 2020-09-14T18:16:35-03:00
weight: "4"
draft: false
---
{{< notice info >}}
Beta: O PIX ainda está em beta, o que significa que temos um grupo pequeno testando a funcionalidade para que então possamos liberar para todos.
{{< /notice >}}

O Pagamento de um PIX pode ser feito através da inserção dos dados completos do recebedor, por meio da inserção de uma chave PIX ou pela leitura de um QR code.

#### Inserção dos dados completos do recebedor:

##### Exemplo de requisição:
```
POST /api/v1/pix_payments
authorization: subject application:participante
content-type: application/json
```

```json
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

##### Exemplo de resposta:
```
201 CREATED
```

```json
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
