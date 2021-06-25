---
title: "Criar chaves (Draft)"
linkTitle: "Criar chaves (Draft)"
date: 2021-07-15T15:00:00-03:00
lastmod: 2021-07-15T15:00:00-03:00
weight: 2
draft: true
description: >

---
Esse médodo deve ser usado quando o dado a ser usado como identificador da Chave PIX ainda não foi cadastrado junto ao DICT ou o cadastro já está inativo. Em casos em que o dado já está sendo utilizado em uma Chave Pix ativa deve ser feita uma [reivindicação](https://stone-co.github.io/docs/pix/chaves-pix/reivindicar/) da Chave PIX. 
<br><br>

##### **Request**

```http
POST /api/v1/pix/:account_id/entries
content-type: application/json
```
Body
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

```http
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

```http
400 BAD REQUEST
```

---

```http
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


##### **Webhook**

Serão disparados webhooks quando o status da solicitação sofrer alterações. Veja [aqui](https://stone-co.github.io/docs/pix/chaves-pix/status/#status-das-solicita%C3%A7%C3%B5es-cria%C3%A7%C3%A3o-e-exclus%C3%A3o) os possíveis status para uma solicitação.

As seguintes informações virão no campo `target_data`.

```text
{
  "id": "cee2f003-95a0-433f-a785-b933a5832531",
  "request_id": uuid(),
  "key": "+5510998765432",
  "key_type": "phone",
  "key_status": "active”,
  "beneficiary_id": "bad7ab7e-f95d-11ea-adc1-0242ac120002",
  "created_at": "20200-09-18T03:00:00Z",
  "error_description": "",
  "status": "accepted"
}
```
<br> <br> 
