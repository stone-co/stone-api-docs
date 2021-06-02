---
title: "Operações Agendadas"
linkTitle: "Operações Agendadas"
slug: "operações-agendadas"
draft: false
date: 2021-05-25T17:00:00-03:00
lastmod: 2021-05-25T17:00:00-03:00
description: >
---
<br>

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

#### **Responses**
---

<br> **Transferência interna**

```JSON
200 OK
content-type: application/json
```

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

<br> **Transferência externa**

```JSON
200 OK
content-type: application/json
```

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
                    "account_code": "10022294",
                    "branch_code": "4208",
                    "institution": "90400888",
                    "institution_name": "BANCO SANTANDER (BRASIL) S.A."
                },
                "entity": {
                    "document": "12409265707",
                    "document_type": "cpf",
                    "name": "Gabi"
                }
            },
            "created_at": "2021-06-02T19:19:00Z",
            "delayed_to_next_business_day": false,
            "fee_amount": 0,
            "operation": "debit",
            "operation_amount": 1,
            "operation_id": "7dd83a74-7e44-4263-8925-6d5e66ba7444",
            "scheduled_to_effective": "2021-06-04",
            "scheduled_to_requested": "2021-06-04",
            "status": "SCHEDULED",
            "type": "external"
        }
    ]
} 
```

<br> **Pagamento**

```JSON
200 OK
content-type: application/json
```

```JSON
{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 25
    },
    "data": [
        {
            "amount": -2000,
            "barcode": "19798864100000020000000001238028677662514706",
            "created_at": "2021-06-02T19:20:53Z",
            "details": {
                "bank_name": null,
                "expiration_date": "2021-06-04",
                "recipient_cpf_cnpj": "92961229022",
                "recipient_name": "Nome do CPF 92961229022",
                "writable_line": "19790000050123802867276625147061886410000002000"
            },
            "fee_amount": 0,
            "operation": "debit",
            "operation_amount": 2000,
            "operation_id": "7ee2777f-5fd2-4f72-a5e9-071787964dd8",
            "scheduled_to": "2021-06-04",
            "status": "SCHEDULED",
            "type": "payment",
            "writable_line": "19790000050123802867276625147061886410000002000"
        }
    ]
} 
```

---
##### **Mensagens de erro**

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
