---
title: "`/POST`Criar uma Chave PIX"
linkTitle: "`/POST`Criar uma Chave PIX"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 2
description: >

---

#### Request

```json5
POST /api/v1/pix_entries
content-type: application/json
{
  "key": “+5510998765432”, 
  "key_type": “phone”, 
  "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
  "participant_ispb": “1234567890”,
  "beneficiary_type": “external_account”,
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "created_at": "2019-11-18T03:00:00Z"
  },
  "beneficiary_entity": {
     "name":"Maria Clara Gomes",
     "document_type": "cpf",
     "document": “13152256685”
  }
}
```
