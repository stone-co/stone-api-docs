---
title: "Reivindicar"
linkTitle: "Reivindicar"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 7
draft: false
description: >

---
Existem cenários em que o dado a ser usado como identificador da Chave PIX já foi cadastrado junto ao DICT e pertence a uma chave ativa, nesses caso não deve ser feita uma criação do zero e sim uma reivindicação da Chave PIX. 
<br><br>
As reivindicações se dividem dem dois tipos:
- `portability`: o dado já esta cadastrado em uma Chave PIX de mesma titularidade em outra instituição. Assim o solicitante deseja apenas que seu dado passe a ser atrelado a Chape PIX da instituição que está pedidno a portabilidade. 
Disponível para os tipos: `phone`, `email`, `cpf` e `cnpj`.
- `ownership`: o dados já está cadastrado em uma chave PIX de outra titularidade. Esse cenário pode aocntecer quando um número de celular, por exemplo, passa a ter um novo dono. 
Disponível para os tipos: `phone`e `email`.


##### **Request**

```http request
POST /api/v1/pix/:account_id/entry_claims
```
Body
```text
{
  "key_type": “phone”, 
  “claim_type”: “portability”,
  "participant_ispb": “1234567890”,
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

Serão disparados webhooks quando o status da reivindicação sofrer alterações. Veja [aqui](https://stone-co.github.io/docs/pix/chaves-pix/status/#status-da-reivindica%C3%A7%C3%A3o) os possíveis status para uma reivindicação. 

As seguintes informações virão no campo `target_data`.

```text
{
  "claim_id": "6c8e9fb9-1416-434d-9933-a36fb3ad7a8c",
  "status": "open"
}
```
<br> <br> 
