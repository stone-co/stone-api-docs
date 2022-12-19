---
title: "Listagem de Reivindicação"
linkTitle: "Listagem de Reivindicação"
date: 2022-09-17T18:00:00-03:00
lastmod: 2022-11-23T11:00:00-03:00
weight: 10
draft: false
description: >

---
<br>

Esse endpoint tem como finalidade listar todas as reivindicações do usuário.

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

**key** `string`
<br>Chave Pix
<br>

**direction** `string`
<br>Valores permitidos: `outbound`, `inbound` 
<br>

**before** `string`
<br> Cursor opaco da paginação.

<br>

**after** `string`
<br> Cursor opaco da paginação.

<br>

**limit** `integer`
<br> Limite de itens retornados.

<br>


##### **Response**
---

```
200 OK
```

Body

```json
{
  "cursor": {"after": null, "before": null, "limit": 25},
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
<br>


```
401 Unauthenticated
```

Usuário não autenticado
<br>
Body
```json
{  
    "type": "srn:error:unauthenticated"
}
```
<br> 
