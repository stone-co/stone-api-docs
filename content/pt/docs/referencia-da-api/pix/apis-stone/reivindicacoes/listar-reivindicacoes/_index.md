---
title: "Listagem de Reivindicação/Portabilidade"
linkTitle: "Listagem de Reivindicação/Portabilidade"
date: 2022-09-17T18:00:00-03:00
lastmod: 2022-11-23T11:00:00-03:00
weight: 10
draft: true
description: Listar as reivindicação/portabilidade>

---

##### **Request**
---

```
GET /api/v1/pix/:account_id/entry_claims
```

##### **Query Params**
---
```
"status"
"key"
"direction"
"limit"
"after"
"before" 
```

<br>

**status** `array` `string` 
Valores permitidos: `open`,  `waiting_resolution`, `confirmed`  , `cancelled` ou `completed`  
<br>

**direction** `string`
<br>Valores permitidos: `outbound`, `inbound` 
<br>


Exemplo:  

- `GET -/api/v1/pix/:account_id/entry_claim?key[]=35425517084&key[]=93744525023`;
<br> <br> 


##### **Response**
---

```
202 ACCEPTED
```
Body
```json
{
  "cursor": {},
  "data": [
   
    {
      "id": "uuid",
      "claim_type": "ownership" | "portability",
      "account_id": "uuid",
      "status": "String",
      "direction": "outbound" | "inbound",
      "donor_participant_ispb": "String",
      "claimer_participant_ispb": "String",
      "created_at": "Datetime",
      "updated_at": "Datetime",
      "expires_at": "Datetime",
      "completion_period_ends_at": "Datetime",
      "resolution_period_ends_at": "Datetime",
      "beneficiary_account": {
        "branch_code": "String",
        "account_code": "String",
        "account_type":"String",
        "opened_at": "Datetime"
      },
      "beneficiary_entity": {
        "name": "String",
        "document_type": "String",
        "document": "String",
      },
      "key_type": "String",
      "key": "String"
    }
  ]
}
```
<br> <br> 


---
```
"waiting_resolution", 
"open",  
"confirmed", 
"automatically_confirmed"
"automatically_confirmed_waiting_resolution",  
"cancel_requested", 
"cancelled",
"automatically_cancelled"
```
<br><br>