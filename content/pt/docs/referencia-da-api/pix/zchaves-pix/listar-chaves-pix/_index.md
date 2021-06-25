---
title: "Listar"
linkTitle: "Listar"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 6
draft: false
description: >

---

##### **Request**

```
GET /api/v1/pix/:account_id/entries
```
Parâmetros para query. 
```
- "participant_ispb" *(obrigatório para participantes indiretos)
- "beneficiary_entity_name"
- "beneficiary_entity_document_type"
- "beneficiary_entity_document"
- "beneficiary_account_branch_code"
- "beneficiary_account_account_code"
- "beneficiary_account_account_type"
- "beneficiary_account_created_at"
- "status"
```
<br> <br> 

##### **Response**

```
200 OK
```
Body
```json
{
  "cursor": {},
  "data": [
    {
      "id": "d990cc41-e514-4343-a84c-80c677102b17",
      "key": "+5510998765432", 
      "key_type": "phone",
      "key_status": "active",
      "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
      "participant_ispb": "1234567890",
      "beneficiary_account": {
        "branch_code": "0001",
        "account_code": "00016583",
        "account_type": "CC",
        "created_at": "2019-11-18T03:00:00Z"
      },
      "beneficiary_entity": {
        "name":"Maria Clara Gomes",
        "document_type": "cpf",
        "document": "13152256685"
      }
    },
    {
      "id": "8544718e-3c76-49ab-bc69-b367d2654a08",
      "key": "lucas@stone.com.br", 
      "key_type": "email",
      "key_status": "active",
      "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
      "participant_ispb": "1234567890",
      "beneficiary_account": {
        "branch_code": "0001",
        "account_code": "00016576",
        "account_type": "CC",
        "created_at": "2019-12-03T03:00:00Z"
      },
      "beneficiary_entity": {
        "name":"Lucas Costa",
        "document_type": "cpf",
        "document": "31152256696"
      }
    }
  ]
}
```
<br> <br> 
