---
title: "Consultar Uma Entrada no Extrato"
slug: "consultar-uma-entrada-no-extrato"
hidden: false
date: 2019-04-01T18:19:45.163Z
lastmod: 2019-12-02T22:56:58.128Z
weight: 9
---

---

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/statement/entries/entry_id
```

<br>

**PATH PARAMS**

---

<br>

**entry_id**  `string`<br>
Identificador da entrada.

<br>

##### Response
---

```
201 OK
content-type: application/json
```
<br>

##### Body
---

```json

{
    "amount": -5400,
    "balance_after": 9992900,
    "balance_before": 9998300,
    "counter_party": {
        "account": {
            "account_code": "10842258",
            "branch_code": "3223",
            "institution": "90400888",
            "institution_name": "Banco Santander (Brasil) S. A."
        },
        "entity": {
            "document": "37818425098",
            "document_type": "cpf",
            "name": "João Amigavel"
        }
    },
    "created_at": "2019-07-31T19:15:00Z",
    "delayed_to_next_business_day": false,
    "fee_amount": 400,
    "id": "cf88fb2e-6026-43d8-8d66-1a7283fd8512",
    "operation": "debit",
    "operation_amount": 5000,
    "operation_id": "0fa4b070-599b-47c1-b03b-541432f24dea",
    "refund_reason_code": null,
    "refund_reason_description": null,
    "scheduled_at": null,
    "scheduled_to_effective": null,
    "scheduled_to_requested": null,
    "status": "FINISHED",
    "type": "external"
}
```
