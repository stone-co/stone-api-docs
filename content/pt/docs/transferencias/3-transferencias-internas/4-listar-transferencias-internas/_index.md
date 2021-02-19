---
title: "Listar Transferências Internas"
slug: "listar-transferências-internas"
draft: false
weight: 4
createdAt: "2019-04-01T19:21:13.323Z"
updatedAt: "2019-12-02T22:56:58.137Z"
---
---
```http request
GET https://sandbox-api.openbank.stone.com.br/api/v1/internal_transfers
```
---

#### QUERY PARAMS
---

**account_id*** `string`
<br>Identificador da conta.

---
**before*** `string`
<br>Cursor opaco da paginação.

---
**after*** `string`
<br>Cursor opaco da paginação.

---
**limit*** `int32`
<br>Limite de itens retornados.

---
**status*** `string`
<br>Allowed values: `SCHEDULE`


<br>

##### **Response**

```JSON
200 OK
content-type: application/json
```
Body
```JSON
{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 25
    },
    "data": [
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
                    "name": "Marcus Oliveira"
                }
            },
            "target_account_code": "58859",
            "target_account_owner_name": "Marcus Oliveira"
        },
        {
            "amount": 1600,
            "approval_expired_at": null,
            "approved_at": "2019-07-31T19:13:55Z",
            "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "cancelled_at": null,
            "created_at": "2019-07-31T19:13:55Z",
            "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "description": "",
            "failed_at": null,
            "failure_reason_code": null,
            "failure_reason_description": null,
            "fee": 0,
            "finished_at": "2019-07-31T19:13:56Z",
            "id": "4aab75b9-c15f-4d27-82e2-ec9c549c1cd8",
            "rejected_at": null,
            "rejected_by": null,
            "scheduled_to": null,
            "settled_at": "2019-07-31T19:13:56Z",
            "status": "FINISHED",
            "target": {
                "account": {
                    "account_code": "58859"
                },
                "entity": {
                    "name": "Marcus Oliveira"
                }
            },
            "target_account_code": "58859",
            "target_account_owner_name": "Marcus Oliveira"
        }
    ]
}