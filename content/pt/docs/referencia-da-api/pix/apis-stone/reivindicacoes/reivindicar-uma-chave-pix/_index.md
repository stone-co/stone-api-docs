---
title: "Reivindicar"
linkTitle: "Reivindicar"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 7
draft: true
description: >

---
Existem cenários em que o dado a ser usado como identificador da Chave Pix já foi cadastrado junto ao DICT e pertence a uma chave ativa, nesses caso não deve ser feita uma criação do zero e sim uma reivindicação da Chave Pix.
<br><br>
As reivindicações se dividem dem dois tipos:
- `portability`: o dado já esta cadastrado em uma Chave Pix de mesma titularidade em outra instituição. Assim o solicitante deseja apenas que seu dado passe a ser atrelado a Chape Pix da instituição que está pedidno a portabilidade.
Disponível para os tipos: `phone`, `email`, `cpf` e `cnpj`.
- `ownership`: o dados já está cadastrado em uma chave Pix de outra titularidade. Esse cenário pode aocntecer quando um número de celular, por exemplo, passa a ter um novo dono.
Disponível para os tipos: `phone`e `email`.


##### **Request**

```
POST /api/v1/pix/:account_id/entry_claims
```
Body
```json
{
  "key_type": "phone",
  "claim_type": "portability",
  "participant_ispb": "1234567890",
  "beneficiary_account": {
     "branch_code": "0001",
     "account_code": "00016583",
     "account_type": "CC",
     "opened_at": "2019-11-18T03:00:00Z"
  },
  "beneficiary_entity": {
     "name": "0001",
     "document_type": "cpf",
     "document": "13152256685"
  }
}
```
<br> <br>

##### **Response**

```
202 ACCEPTED
```
Body
```json
{
  "claim_id": "6c8e9fb9-1416-434d-9933-a36fb3ad7a8c",
  "claim_type": "portability"
}
```
<br> <br>


##### **Webhook**

Serão disparados webhooks quando o status da reivindicação sofrer alterações. Veja [aqui](https://stone-co.github.io/docs/pix/chaves-pix/status/#status-da-reivindica%C3%A7%C3%A3o) os possíveis status para uma reivindicação.

As seguintes informações virão no campo `target_data`.

```json
{
  "claim_id": "6c8e9fb9-1416-434d-9933-a36fb3ad7a8c",
  "status": "open"
}
```
<br> <br>
