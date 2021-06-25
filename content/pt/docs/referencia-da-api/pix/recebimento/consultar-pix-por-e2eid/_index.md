---
title: "Consultar Pix recebido pelo end_to_end_id (Draft)"
linkTitle: "Consultar Pix recebido pelo end_to_end_id (Draft)"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-06-16T15:17:00-03:00
weight: 4
draft: true
description: >
  
---

Através desse endpoint será possível consultar um Pix recebido através do end_to_end_id. Segue padrão definido pelo Banco Central.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{e2eid}}
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **PATH PARAMS**
---
<br>

**e2eid*** `string`

<br>
Exemplo:

```json
{
  "type": "object",
  "properties": {
    "e2eid": {
      "type": "string",
      "required": true
    }
  },
  "required": [
    "e2eid"
  ]
}
```
<br>

##### **Response**
---

```json
200 OK
```

```json
{
  "devolucoes": [
    {
      "horario": {
        "liquidacao": "2021-03-23T10:53:09.612326Z",
        "solicitacao": "2021-03-23T10:53:09.060862Z"
      },
      "id": "maroto123",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D1650155520210323105348b6cffe3d3",
      "status": "DEVOLVIDO",
      "valor": "30.00"
    },
    {
      "horario": {
        "liquidacao": "2021-03-23T11:15:23.876470Z",
        "solicitacao": "2021-03-23T11:15:23.529061Z"
      },
      "id": "12maroto123",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D165015552021032311153d55484949a",
      "status": "DEVOLVIDO",
      "valor": "30.00"
    },
    {
      "horario": {
        "liquidacao": "2021-03-23T23:29:43.140578Z",
        "solicitacao": "2021-03-23T23:29:42.125167Z"
      },
      "id": "anyId588",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D16501555202103232329d08247741e6",
      "status": "DEVOLVIDO",
      "valor": "10.00"
    },
    {
      "horario": {
        "liquidacao": null,
        "solicitacao": "2021-03-30T21:06:42.619471Z"
      },
      "id": "anyId121",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D165015552021033021063ed204590ae",
      "status": "EM_PROCESSAMENTO",
      "valor": "0.01"
    },
    {
      "horario": {
        "liquidacao": "2021-03-23T23:32:47.709407Z",
        "solicitacao": "2021-03-23T23:32:47.352844Z"
      },
      "id": "anyId7",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D1650155520210323233273b0a425d19",
      "status": "DEVOLVIDO",
      "valor": "0.01"
    },
    {
      "horario": {
        "liquidacao": "2021-03-23T23:34:11.078161Z",
        "solicitacao": "2021-03-23T23:34:10.644294Z"
      },
      "id": "anyId135",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D16501555202103232334200fc5764e4",
      "status": "DEVOLVIDO",
      "valor": "0.01"
    },
    {
      "horario": {
        "liquidacao": null,
        "solicitacao": "2021-04-01T21:17:34.282042Z"
      },
      "id": "anyId967",
      "motivo": "Devolução solicitada pelo usuário recebedor do pagamento original",
      "rtrId": "D1650155520210401211705b9aea4f46",
      "status": "EM_PROCESSAMENTO",
      "valor": "0.01"
    }
  ],
  "endToEndId": "E165015552021021523376414ac8f718",
  "horario": "2021-02-15T23:41:17.870349Z",
  "infoPagador": null,
  "txid": null,
  "valor": "1300.00"
}
```