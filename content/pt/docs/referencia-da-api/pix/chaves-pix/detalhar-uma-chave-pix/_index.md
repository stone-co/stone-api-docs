---
title: "Detalhar chave Pix"
linkTitle: "Detalhar chave Pix"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 4
draft: false
description: >

---
<br>
Esse endpoint deve ser chamado para detalhar uma chave Pix. <br><br>


```
GET /api/v1/pix/{{account_id}}/entries/{{id}}?participant_ispb=xxxx
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

##### **QUERY PARAMS**
---

**account_id** `string`
<br> Identificador da conta

**id** `string`
<br> Identificador da chave a ser deletada. Caso não saiba o `id` da chave, liste as chaves da conta por esse [endpoint]({{< relref "/docs/referencia-da-api/pix/chaves-pix/listar-chaves-pix/">}}) e pegue o `id`.
<br><br>

Parâmetros (filtros) para a query: 
- "participant_ispb" *(obrigatório para participantes indiretos)
- "beneficiary_entity_name"
- "beneficiary_entity_document_type"
- "beneficiary_entity_document"
- "beneficiary_account_branch_code"
- "beneficiary_account_account_code"
- "beneficiary_account_account_type"
- "beneficiary_account_created_at"
- "status"
<br><br>

##### **RESPONSE**
---

```
200 OK
```
<br>

**Body**
```json
{
  "id": d990cc41-e514-4343-a84c-80c677102b17,
  "key": “+5510998765432”, 
  "key_type": "phone", 
  "key_status": "active",
  "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
  "participant_ispb": “1234567890”,
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "created_at": "2019-11-18T03:00:00Z"
  },
  "beneficiary_entity": {
     "name":"Maria Clara Gomes",
     "document_type": "cpf",
     "document": “13152256685”
  }, 
  "events": [
    {
      "id": 38963369-533c-42aa-a49e-b5369ff4bd52,
      "created_at": "20200-09-18T03:00:00Z",
      "type": "created",
      "from_status": null,
      "to_status": "active"
    },
    {
      "id": 7eb6ee15-1485-468a-ad38-411320878815,
      "created_at": “20200-09-22T03:00:00Z”,
      "type": "deleted",
      "from_status": "active",
      "to_status": "deleted"
    }
  ]
}
```