---
title: "Listar Transferências Externas"
slug: "listar-transferências-externas"
draft: false
weight: 8
date: "2019-04-01T19:31:32.470Z"
lastmod: "2019-12-02T22:56:58.144Z"
---
```http request
GET https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers
```
---

#### **QUERY PARAMS**
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
    },
    {
      "amount": 5000,
      "approval_expired_at": null,
      "approved_at": "2019-07-31T19:15:00Z",
      "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
      "cancelled_at": null,
      "created_at": "2019-07-31T19:15:00Z",
      "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
      "delayed_to_next_business_day": false,
      "failed_at": null,
      "failure_reason_code": null,
      "failure_reason_description": null,
      "fee": 400,
      "finished_at": "2019-07-31T19:15:01Z",
      "id": "0fa4b070-599b-47c1-b03b-541432f24dea",
      "refund_reason_code": null,
      "refund_reason_description": null,
      "refunded_at": null,
      "rejected_at": null,
      "rejected_by": null,
      "scheduled_to_effective": null,
      "scheduled_to_requested": null,
      "settled_at": "2019-07-31T19:15:01Z",
      "status": "FINISHED",
      "target": {
        "account": {
          "account_code": "10842258",
          "branch_code": "3223",
          "institution_code": "90400888",
          "institution_ispb": "90400888",
          "institution_name": "Banco Santander (Brasil) S. A.",
          "institution_number_code": "033"
        },
        "entity": {
          "cpf": "37818425098",
          "document": "37818425098",
          "document_type": "cpf",
          "name": "Jo\u00e3o Amigavel"
        }
      }
    }
  ]
}
