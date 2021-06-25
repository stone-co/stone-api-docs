---
title: "Listar pagamento de folha"
slug: "listar-pagamento-de-folha"
draft: false
weight: 1
date: "2019-09-12T16:43:22.234Z"
lastmod: "2019-09-16T19:01:55.439Z"
---
---

``` 
GET https://sandbox-api.openbank.stone.com.br/api/v1/payrolls
```
---

#### **QUERY PARAMS**

---

**account_id**  `string`
<br> Identificador da conta no formato UUID.

{{% pageinfo %}}
**Paginação**
<br>Este endpoint utiliza paginação. Para mais informações, acesse [aqui](/docs/referencia-da-api/stone-openbank/paginacao)
{{% /pageinfo %}}


<br>

#### **Response**

```json
200 OK
content-type: application/json
```
Body
```json
{
  "cursor": {
    "after": null,
    "before": null,
    "limit": 25
  },
  "data": [
    {
      "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
      "amount": 1,
      "created_at": "2019-07-15T17:08:52Z",
      "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
      "fee": 0,
      "id": "bee7f841-a5b1-4672-b6e5-0742612dfa33",
      "outside_operating_hours": null,
      "status": "FINISHED",
      "summary": {
        "number_of_failed_salaries": 0,
        "number_of_finished_salaries": 1,
        "number_of_refunded_salaries": 0,
        "number_of_salaries": 1,
        "number_of_scheduled_salaries": 0
      }
    },
    {
      "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
      "amount": 100,
      "created_at": "2019-08-28T12:30:11Z",
      "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
      "fee": 0,
      "id": "99b4bba8-59b4-465b-8ebe-68be41edc031",
      "outside_operating_hours": null,
      "status": "CREATED",
      "summary": {
        "number_of_failed_salaries": 7,
        "number_of_finished_salaries": 0,
        "number_of_refunded_salaries": 0,
        "number_of_salaries": 8,
        "number_of_scheduled_salaries": 0
      }
    }
  ]
}
