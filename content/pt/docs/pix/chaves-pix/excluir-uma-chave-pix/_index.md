---
title: "Excluir"
linkTitle: "Excluir"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 4
draft: false
description: >
   
---

No caso de PSPs diretos e indiretos existem situações em que é necessária a exclusão de uma Chave PIX como, as principais são:
- conta foi encerrada no PSP;
- portabilidade cedida a outra instituição;
- posse cedida a outra instituição/usuário.


##### **Request**

```http request
DELETE /api/v1/pix/:account_id/entries/:id
```
Body
```text
{
  "key_type": “phone”,
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

```http request
202 ACCEPTED
content-type: application/json
```
Body
```text
{
  "id": “4b612bce-f964-11ea-adc1-0242ac120002”
}
```
<br> <br> 


##### **Webhook**
Serão disparados webhooks quando o status da solicitação sofrer alterações. Veja [aqui](https://stone-co.github.io/docs/pix/chaves-pix/status/#status-das-solicita%C3%A7%C3%B5es-cria%C3%A7%C3%A3o-e-exclus%C3%A3o) os possíveis status para uma solicitação.

As seguintes informações virão no campo `target_data`.

```text
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
