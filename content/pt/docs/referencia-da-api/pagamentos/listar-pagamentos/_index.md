---
title: "Listar Pagamentos"
slug: "listar-pagamentos"
hidden: false
date: "2019-04-01T19:38:57.844Z"
lastmod: "2019-12-02T22:56:58.154Z"
weight: 4
---
---

``` 
GET https://sandbox-api.openbank.stone.com.br/api/v1/payments
```
---

#### **QUERY PARAMS**

---

<br>

**account_id***  `string` 

Identificador da conta.


---
<br>

**before***  `string` 

Cursor opaco da paginação.


---

<br>

**after***  `string` 

Cursor opaco da paginação.


---
<br>

**limit***  `int32` 

Limit de itens retornados.

<br>


##### **Response**

```json
200 OK 
```
Body
```json
{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 25,
        "total_count": null,
        "total_count_cap_exceeded": null
    },
    "data": [
        {
            "account_id": "8cbeb3d2-750f-4b14-81a1-143ad715c273",
            "amount": 100,
            "approval_expired_at": null,
            "approved_at": "2019-08-02T18:25:20Z",
            "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "barcode": "89640000000010003139146877284281444986767347",
            "cancelled_at": null,
            "created_at": "2019-08-02T18:25:20Z",
            "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "details": {
                "bank_name": null,
                "expiration_date": null,
                "recipient_cpf_cnpj": "89581759239",
                "recipient_name": "Ana Sophia de Lara"
            },
            "failed_at": null,
            "failure_reason_code": null,
            "failure_reason_description": null,
            "fee": 0,
            "finished_at": "2019-08-02T18:25:21Z",
            "id": "3f799fb7-ed0b-4bbe-be0e-575d0075f69d",
            "refunded_at": null,
            "rejected_at": null,
            "rejected_by": null,
            "scheduled_to": null,
            "status": "FINISHED",
            "writable_line": "896400000007010003139143687728428149449867673476"
        },
        {
            "account_id": "8cbeb3d2-750f-4b14-81a1-143ad715c273",
            "amount": 100,
            "approval_expired_at": null,
            "approved_at": "2019-08-02T18:23:58Z",
            "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "barcode": "89670000000010003137498189637166095077491613",
            "cancelled_at": null,
            "created_at": "2019-08-02T18:23:58Z",
            "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "details": {
                "bank_name": null,
                "expiration_date": null,
                "recipient_cpf_cnpj": "17085470968",
                "recipient_name": "Paulo da Penha"
            },
            "failed_at": null,
            "failure_reason_code": null,
            "failure_reason_description": null,
            "fee": 0,
            "finished_at": "2019-08-02T18:23:59Z",
            "id": "851e9719-ed26-4627-a7d4-02b54d896d54",
            "refunded_at": "2019-08-02T18:24:01Z",
            "rejected_at": null,
            "rejected_by": null,
            "scheduled_to": null,
            "status": "REFUNDED",
            "writable_line": "896700000004010003137493818963716605950774916130"
        },
        {
            "account_id": "8cbeb3d2-750f-4b14-81a1-143ad715c273",
            "amount": 100,
            "approval_expired_at": null,
            "approved_at": "2019-07-31T19:12:51Z",
            "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "barcode": "89690000000010003139343476533694034641055662",
            "cancelled_at": null,
            "created_at": "2019-07-31T19:12:51Z",
            "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
            "details": {
                "bank_name": null,
                "expiration_date": null,
                "recipient_cpf_cnpj": "90890860998",
                "recipient_name": "Sr. Luiz Bulhões"
            },
            "failed_at": null,
            "failure_reason_code": null,
            "failure_reason_description": null,
            "fee": 0,
            "finished_at": "2019-07-31T19:12:52Z",
            "id": "ace4331a-45ef-488a-9fde-c439739b9d4a",
            "refunded_at": null,
            "rejected_at": null,
            "rejected_by": null,
            "scheduled_to": null,
            "status": "FINISHED",
            "writable_line": "896900000002010003139341347653369400346410556622"
        }
    ]
}
```
