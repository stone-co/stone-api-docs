---
title: "Retornar Um Pagamento"
slug: "retornar-um-pagamento"
hidden: false
date: "2019-04-01T19:40:49.193Z"
lastmod: "2019-12-02T22:56:58.156Z"
weight: 5
---


```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/payments/payment_id
```
---

**PATH PARAMS**

---

**payment_id***  `string` 

Identificador do pagamento.

<br>

---

##### **Response**

```JSON
200 ok 
```

```JSON
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
}
```
