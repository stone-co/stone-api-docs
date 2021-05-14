---
title: "Retornar Uma Transferência Externa"
slug: "retornar-uma-transferência-externa"
draft: false
weight: 9
date: "2019-04-01T19:33:33.090Z"
lastmod: "2019-12-02T22:56:58.146Z"
---

---
<br>

```http request
GET https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers/transfer_id
```
---

#### **PATH PARAMS**
---
<br>

**transfer_id*** `string`
<br>Identificador da transferência externa.



<br>

##### **Response**

```JSON
200 OK
content-type: application/json
```
Body
```JSON
{
    "amount": 100,
    "approval_expired_at": null,
    "approved_at": "2019-08-02T18:14:34Z",
    "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "cancelled_at": null,
    "created_at": "2019-08-02T18:14:34Z",
    "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "delayed_to_next_business_day": false,
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 400,
    "finished_at": "2019-08-02T18:14:34Z",
    "id": "7458c329-c5e9-4cc8-8174-3aa6210a8867",
    "refund_reason_code": null,
    "refund_reason_description": null,
    "refunded_at": null,
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to_effective": null,
    "scheduled_to_requested": null,
    "settled_at": "2019-08-02T18:14:34Z",
    "status": "FINISHED",
    "target": {
        "account": {
            "account_code": "58859",
            "branch_code": "1",
            "institution_code": "90400888",
            "institution_ispb": "90400888",
            "institution_name": "Banco Santander (Brasil) S. A.",
            "institution_number_code": "033"
        },
        "entity": {
            "cpf": "62752545053",
            "document": "62752545053",
            "document_type": "cpf",
            "name": "Octacilio Impoluto"
        }
    }
}
