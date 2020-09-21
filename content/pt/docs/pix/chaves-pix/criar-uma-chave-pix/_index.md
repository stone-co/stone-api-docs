---
title: "Criar"
linkTitle: "Criar"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 3
description: >

---
Esse médodo deve ser usado quando o dado a ser usado como identificador da Chave PIX ainda não foi cadastrado junto ao DICT ou o cadastro já está inativo. Em casos em que o dado já está sendo utilizado em uma Chave PIX ativa deve ser feita uma [reivindicação](https://stone-co.github.io/docs/pix/chaves-pix/reivindicar/) da Chave PIX. 
<br><br>

##### **Request**

```http request
POST /api/v1/pix_entries
content-type: application/json
```
Body
```text
{
  "key": “+5510998765432”, 
  "key_type": “phone”, 
  "account_id": "968cc34d-d827-448b-ac1b-e6e29836a160",
  "participant_ispb": “1234567890”,
  "beneficiary_type": “external_account”,
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
  }
}
```
<br> <br> 

##### **Response**

```http request
202 CONTINUE
content-type: application/json
```
Body
```text
{
  "id": “cee2f003-95a0-433f-a785-b933a5832531”
}
```
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
  "beneficiary_type": "external_account",
  "beneficiary_id": "bad7ab7e-f95d-11ea-adc1-0242ac120002",
  "created_at": "20200-09-18T03:00:00Z",
  "error_description": "",
  "status": "accepted"
}
```
<br> <br> 
