---
title: "Listar chaves Pix"
linkTitle: "Listar chaves Pix"
date: 2021-07-15T14:00:00-03:00
lastmod: 2021-07-15T14:00:00-03:00
weight: 1
draft: false
description: >

---
<br>

Para listar as chaves de uma conta, você deve utilizar o endpoint abaixo:

```
GET /api/v1/pix/{{account_id}}/entries
```
##### **HEADERS**
---

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

**authorization** `string`
<br> Bearer Token

**User-Agent** `string`
<br>Nome da sua aplicacão

<br>

##### **PATH PARAMS**
---

**account_id** `string`
<br> Identificador da conta
<br> <br>

##### **QUERY PARAMS**
---

**status** `string`

<br> Valores permitidos: `key_created`, `portability_claimed`, `ownership_claimed`, `failed` ou `deleted`
<br> <br> 

##### **RESPONSE**
---
```
200 OK
```
<br>

**Body**

```json
{
  "cursor": {},
  "data": [
    {
      "id": "d990cc41-e514-4343-a84c-80c677102b17",
      "key": "+5510998765432", 
      "key_type": "phone",
      "key_status": "active",
      "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
      "participant_ispb": "1234567890",
      "beneficiary_account": {
        "branch_code": "0001",
        "account_code": "00016583",
        "account_type": "CC",
        "created_at": "2019-11-18T03:00:00Z"
      },
      "beneficiary_entity": {
        "name":"Maria Clara Gomes",
        "document_type": "cpf",
        "document": "13152256685"
      }
    },
    {
      "id": "8544718e-3c76-49ab-bc69-b367d2654a08",
      "key": "lucas@stone.com.br", 
      "key_type": "email",
      "key_status": "active",
      "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
      "participant_ispb": "1234567890",
      "beneficiary_account": {
        "branch_code": "0001",
        "account_code": "00016576",
        "account_type": "CC",
        "created_at": "2019-12-03T03:00:00Z"
      },
      "beneficiary_entity": {
        "name":"Lucas Costa",
        "document_type": "cpf",
        "document": "31152256696"
      }
    }
  ]
}
```
<br> <br> 
