---
title: "Listar reivindicações"
linkTitle: "Listar reivindicações"
date: 2022-09-17T18:00:00-03:00
lastmod: 2022-11-23T11:00:00-03:00
weight: 10
draft: true
description: >

---

##### **Request**
---

```
GET /api/v1/pix/:account_id/entry_claims
```

##### **Query params**
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
<br>
Valores permitidos:  `waiting_resolution`, `open`, `cancelled`, `completed` ou `confirmed`

<br>

**direction** `string`
<br>
Valores permitidos: `outbound`, `inbound` 


Exemplo:  

- `GET -/api/v1/pix/:account_id/entry_claim?key[]=35425517084&key[]=93744525023`;
<br> <br> 


##### **Response**
---

```
202 CONTINUE
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


##### **Status para direção `outbound`**
---

```
"waiting_resolution", 
"open", 
"failed",  
"confirmed", 
"automatically_confirmed_waiting_resolution",  
"completed", 
"complete_requested", 
"cancel_requested", 
"cancelled"
```
<br><br>
Obs: status a serem considerados pelo front quando a direction é "outbound"
<br>
- `failed` | `cancelled` | `completed`: finalizados
- `confirmed`: precisa exibir uma notificação pro cliente completar ação
- demais status são intermediários: 
    - `open`: criação requisitada
    - `automatically_confirmed_waiting_resolution`: se passaram 7 dias desde a criação da reivindicação, mas o usuario em posse da chave ainda não confirmou (temos que esperar)
    - `cancel_requested`: cancelamento requisitado pelo usuário
    - `complete_requested`: usuário requisitou API de completar, mas ainda não foi completado
<br><br>


##### **Status para direção `inbound`**
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