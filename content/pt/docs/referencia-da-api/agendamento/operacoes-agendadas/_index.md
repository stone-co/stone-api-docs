---
title: "Operações Agendadas"
linkTitle: "Operações Agendadas"
slug: "operações-agendadas"
draft: false
date: 2021-05-25T17:00:00-03:00
lastmod: 2021-05-25T17:00:00-03:00
description: >
---
Este endpoint lista todas as operações agendadas que não foram liquidadas até o momento da consulta.

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/{id}/schedulings
```

---

#### **HEADERS**

---

<br>

**Authorization** `string`
<br>Bearer token

<br>

#### **PATH PARAMS**

---
<br>

**id** `string`
<br>Identificador da conta onde se deseja ver os agendamentos.

<br>

#### **QUERY PARAMS**

---
<br>

**limit**  `int32`

<br>

**before**  `string`<br>
Traz a página anterior ao cursor.

<br>

**after**  `string`<br>
Traz a página posterior ao cursor.

<br><br>

#### **Response**
---

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
            "amount": -1,
            "counter_party": {
                "account": {
                    "account_code": "5053418",
                    "branch_code": "1",
                    "institution": "16501555",
                    "institution_name": "Stone Pagamentos S.A."
                },
                "entity": {
                    "name": "Gabriela Abreu de Andrade"
                }
            },
            "created_at": "2021-05-25T20:26:29Z",
            "description": "",
            "fee_amount": 0,
            "operation": "debit",
            "operation_amount": 1,
            "operation_id": "b6b82602-4d14-4095-ae6b-556df74abcaf",
            "scheduled_to": "2021-05-27",
            "status": "SCHEDULED",
            "type": "internal"
        }
    ]
}
```

---

```JSON
400 Bad Request
content-type: application/json
```

```JSON
{
    "path": "limit",
    "type": "srn:error:invalid_cursor"
}
```
---

```JSON
403 Forbidden
content-type: application/json
```

```JSON
{
    "type": "srn:error:unauthorized"
}
```
