---
title: "Criar chaves Pix"
linkTitle: "Criar chaves Pix"
date: 2021-08-12T19:00:00-03:00
lastmod: 2021-10-14T09:26:00-03:00
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

<br>

##### **BODY PARAMS**
---
<br>

**- Para criar uma chave aleatória**


```json
{
    "key": "",
    "key_type": "random_key",
    "participant_ispb": "16501555"
}
```
<br> <br> 

**- Para criar uma chave de documento**


```json
{
    "key": "número-do-documento",
    "key_type": "cpf-ou-cnpj",
    "participant_ispb": "16501555"
}
```
Ex: 
```json
{
    "key": "12409265707",
    "key_type": "cpf",
    "participant_ispb": "16501555"
}
```


<br> <br> 
##### **Response**
---

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

<br>

Body
```json
{
  "type": "srn:error:entries_limit_reached"
}
```
Acontece quando o limite de chaves para a conta foi atingido
<br> <br> 

