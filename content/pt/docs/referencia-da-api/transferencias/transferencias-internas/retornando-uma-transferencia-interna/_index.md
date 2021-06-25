---
title: "Retornando uma Transferência Interna"
slug: "retornando-uma-transferência-interna"
draft: false
weight: 5
date: "2019-04-01T19:23:33.248Z"
lastmod: "2019-12-02T22:56:58.139Z"
---
---
<br>

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/internal_transfers/transfer_id
```
<br>

#### **PATH PARAMS**
---
<br>

**transfer_id** `string`
<br>Identificador da transferência.


<br> 

##### **Response**

```json
200 OK
content-type: application/json
```
Body
```json
{
    "amount": 100,
    "approval_expired_at": null,
    "approved_at": "2019-08-02T18:00:27Z",
    "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "cancelled_at": null,
    "created_at": "2019-08-02T18:00:27Z",
    "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "description": "",
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "finished_at": "2019-08-02T18:00:28Z",
    "id": "c97de6a6-a35a-423d-a3df-add006a0038e",
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to": null,
    "settled_at": "2019-08-02T18:00:28Z",
    "status": "FINISHED",
    "target": {
        "account": {
            "account_code": "58859"
        },
        "entity": {
            "name": "Antonio Nunes"
        }
    },
    "target_account_code": "58859",
    "target_account_owner_name": "Antonio Nunes"
}
