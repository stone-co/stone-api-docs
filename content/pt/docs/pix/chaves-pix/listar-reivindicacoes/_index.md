---
title: "Listar reivindicações"
linkTitle: "Listar reivindicações"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 10
draft: false
description: >

---

##### **Request**

```http request
GET /api/v1/pix/:account_id/entry_claims
```
Parâmetros para query.
```text
- "participant_ispb" *(obrigatório para participantes indiretos)
- "claim_type"
- "origin"
- "origin_ispb" (quando origin é external)
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

```http request
202 CONTINUE
```
Body
```text
{
  "cursor": {},
  "data": [
    {
      "id": "40346adc-74f3-4c4e-8275-73ba78993491",
      “claim_type”: “portability”,
      "status": "open",
      "origin": "external",
      "origin_ispb": "9876543210",
      “created_at”: "“2020-09-27T03:00:00Z”,
      “updated_at”: "2020-09-27T06:00:00Z", 
      “expiration_at”: "2020-09-30T03:00:00Z",
      "beneficiary_account": {
        "branch_code": “0001”,
        "account_code": "00016583",
        "account_type": "CC",
        "opened_at": "2019-11-18T03:00:00Z"
      },
      "beneficiary_entity": {
        "name":"Maria Clara Gomes",
        "document_type": "cpf",
        "document": “13152256685”
      },
      "key": “+5510998765432”, 
      "key_type": "phone"
    }
  ]
}
```
<br> <br> 
