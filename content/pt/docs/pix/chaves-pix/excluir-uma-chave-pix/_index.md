---
title: "Excluir"
linkTitle: "Excluir"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 4
description: >
   
---

No caso de PSP diretos e indiretos existem situações em que é necessária a exclusão de uma Chave PIX como, por exemplo, no encerramento de uma conta.

##### **Request**

```json5
DELETE /api/v1/pix_entries/key/:id
{
  "key_type": “phone”,
  “account_id”: “968cc34d-d827-448b-ac1b-e6e29836a160”,
  "participant_ispb": “1234567890”,
  "beneficiary_type": “external_account”,
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "opened_at": "2019-11-18T03:00:00Z"
  },
  "reason": "user_requested”
}
```
<br> <br> 

##### **Response**

```json5
202 CONTINUE
content-type: application/json
{
  "id": “4b612bce-f964-11ea-adc1-0242ac120002”
}
```
<br> <br> 


##### **Webhook**

Serão disparados webhooks quando o status da solicitação alterar para `accepted`ou `rejected`.
As seguintes informações virão no campo `target_data`.

```json5
{
  "id": “4b612bce-f964-11ea-adc1-0242ac120002”
  “key”: “+5510998765432”,
  “key_type”: "phone"
  “key_status”: “deleted”,
  “beneficiary_type”: "external_account",
  “beneficiary_id”: “bad7ab7e-f95d-11ea-adc1-0242ac120002”,
   "created_at": “20200- 09-18T03:00:00Z”,
   "error_description": “”,
   "status": “accepted"
}
```
<br> <br> 
