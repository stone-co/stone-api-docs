---
title: "Listar Relatos de Infrações recebidos"
linkTitle: "Listar Relatos de Infrações recebidos"
date: 2022-02-11T15:17:00-03:00
lastmod: 2022-02-11T09:09:00-03:00
weight: 9
description: >
  
---

Através desse endpoint será possível listar todos os Relatos de Infrações recebidos na conta.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{account_id}}/infractions_reports
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **QUERY PATH**
---
<br>

**account_id*** `string`
<br>Identificador da conta

##### **QUERY PARAMS**

**range** `string`
<br>Format: [Num, Num]
<br>Ex: range=[0, 5]

**sort** `string`
<br>Format: [field, "ASC"|"DESC"]
<br>Possible fields: "created_at", "expires_at"
<br>Ex: sort=["created_at", "ASC"]

**filter** `string`
<br>Format: {field: value} (Pode filtar por vários campos ao mesmo tempo)
<br>Possible fields: "type", "reported_by", "status", "analysis_result", "end_to_end_id", "refund_id", "direction"
<br>Ex: filter={"type": "fraud", "reported_by": "debited_participant"}

Exemplo:

```
https://sandbox-api.openbank.stone.com.br/api/v1/pix/477f8576-ca82-462b-be73-dc28cc6490c3
/infractions_reports?range=[0, 5]&sort=["created_at", "ASC"]&filter={"type": "fraud", "reported_by": "debited_participant"}
```
<br>

##### **Response**
---

```
200 OK
```

```json
[
    {
        "accepted_at": null,
        "account_id": "12aa3b3c-d44d-4885-be9a-eccb5d306660",
        "analysis_details": null,
        "analysis_result": null,
        "cancelled_at": null,
        "created_at": "2022-02-10T23:59:11.984877Z",
        "credited_participant": "18727053",
        "debited_participant": "16501555",
        "direction": "inbound",
        "end_to_end_id": "E165015552022020920407aad1c7c239",
        "expires_at": "2022-02-17T23:59:11.984877Z",
        "id": "8715a2ee-9a68-41d4-8a9f-a46f7a814f15",
        "infraction_id": "b182bbce-de10-4bc2-9d03-c11746642ab2",
        "inserted_at": "2022-02-10T23:59:22.249074Z",
        "refund_id": null,
        "rejected_at": null,
        "report_details": "Foi uma fraude",
        "reported_by": "debited_participant",
        "request_id": "ea9ad974-2b9f-49df-b37c-ce67d80d4c8a",
        "status": "pending",
        "transaction_result": "settled",
        "transaction_type": "spi",
        "type": "fraud",
        "updated_at": "2022-02-10T23:59:22.249074Z"
    }
]
```

<br>

```
400 Bad Request
```

```json
{
    "type": "srn:error:invalid account_id path param"
}
```

<br>

```
403 Forbidden
```

```json
{
    "type": "srn:error:unauthorized"
}
```
