---
title: "Aprovar/Rejeitar reivindicação"
linkTitle: "Aprovar/Rejeitar reivindicação"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 8
description: >

---
Quando a usuária faz, em uma outra instituição, a solicitação de portabilidade ou posse da chave que possui junto ao PSP, o mesmo receberá um pedido que deve ser aprovado ou rejeitado pela usuária. 
<br><br>

##### **Webhook**

Ai receber uma reivindicação será disparado o seguinte webhook:

```text
{
  "claim_id": 6c8e9fb9-1416-434d-9933-a36fb3ad7a8c,
  "key_type": "phone",
  "key": "+5510998765432",
  “claim_type”: “portability”,
  "claim_origin_ispb": "9876543210",
  "beneficiary_type": “external_account”,
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "opened_at": "2019-11-18T03:00:00Z"
  },
  "beneficiary_entity": {
     "name": “0001”,
     "document_type": "cpf",
     "document": "13152256685"
  }
}
```
<br> <br> 

##### **Request**

```http request
POST /api/v1/pix_entry_claims/:claim_id/actions/:action {approve|reject}
content-type: application/json
```
<br> <br> 

##### **Response**

```http request
202 CONTINUE
```
Body
```text
{
  "claim_id": “6c8e9fb9-1416-434d-9933-a36fb3ad7a8c”,
  "claim_type": “portability”
}
```
<br> <br> 

##### **Webhook**

Serão disparados webhooks quando o status da reivindicação alterar. As seguintes informações virão no campo target_data.
Veja [aqui](https://stone-co.github.io/docs/pix/chaves-pix/status/#status-da-reivindica%C3%A7%C3%A3o) todos os status de uma reivindicação.

```text
{
  "claim_id": "6c8e9fb9-1416-434d-9933-a36fb3ad7a8c",
  "status": "open"
}
```
<br> <br> 
