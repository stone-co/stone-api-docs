---
title: "Consultar pagamento de folha"
slug: "consultar-pagamento-de-folha"
draft: false
weight: 3
date: "2019-09-12T17:20:23.207Z"
lastmod: "2019-09-12T17:25:16.438Z"
---
---

```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/payrolls/payroll_id
```
---

#### **PATH PARAMS**

---
**payroll_id***  `string`
<br> Identificador da folha no formato UUID.

<br>

#### **Response**

```JSON
200 OK
content-type: application/json
```
Body
```JSON
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "amount": 100,
  "created_at": "2019-09-02T16:23:32Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "fee": 0,
  "id": "4f609244-1329-413c-a666-45efb793a9c2",
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
