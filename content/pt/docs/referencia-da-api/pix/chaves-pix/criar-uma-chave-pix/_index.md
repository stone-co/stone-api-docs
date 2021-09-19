---
title: "Criar chaves Pix"
linkTitle: "Criar chaves Pix"
date: 2021-08-12T19:00:00-03:00
lastmod: 2021-08-12T19:00:00-03:00
weight: 2
draft: false
description: >

---
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{account_id}}/entries
```
<br>

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
<br> <br> 

##### **BODY PARAMS**

```json
{
  "key": "+5510998765432", 
  "key_type": "phone", 
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
}
```
<br> <br> 

##### **Response**

```
202 ACCEPTED
content-type: application/json
```

Body
```json
{
  "id": "cee2f003-95a0-433f-a785-b933a5832531"
}
```

---

```
400 BAD REQUEST
```

---

```
422 DOMAIN ERROR
```

Body
```json
{
  "type": "srn:error:already_exists"
}
```
Acontece quando a chave já foi criada
<br> <br> 

