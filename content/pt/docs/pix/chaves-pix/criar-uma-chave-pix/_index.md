---
title: "Criar"
linkTitle: "Criar"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 3
description: >

---

##### **Request**

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
<br> <br> 

##### **Response**

```json5
202 CONTINUE
content-type: application/json

{
  "id": “cee2f003-95a0-433f-a785-b933a5832531”
}
```
<br> <br> 


##### **Webhook**

Serão disparados webhooks quando o status da solicitação alterar para `accepted`ou `rejected`.
As seguintes informações virão no campo `target_data`.

```json5
{
  "id": "cee2f003-95a0-433f-a785-b933a5832531",
  "request_id": uuid(),
  "key": "+5510998765432",
  "key_type": "phone",
  "key_status": "active”,
  "beneficiary_type": "external_account",
  "beneficiary_id": "bad7ab7e-f95d-11ea-adc1-0242ac120002",
  "created_at": "20200-09-18T03:00:00Z",
  "error_description": "",
  "status": "accepted"
}
```
<br> <br> 
