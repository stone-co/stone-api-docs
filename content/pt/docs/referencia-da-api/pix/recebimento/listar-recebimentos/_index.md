---
title: "Listar Pix recebidos"
linkTitle: "Listar Pix recebidos"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-06-16T15:17:00-03:00
weight: 5
description: >
  
---

Através desse endpoint será possível listar todos os Pix recebidos na conta. Esse endpoint segue os padrões definidos pelo Banco Central.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **QUERY PARAMS**
---
<br>

**inicio*** `string`
<br>Format: date-time

**fim*** `string`
<br>Format: date-time

**txid** `string`

**txidPresente** `boolean`

**devolucaoPresente** `boolean`

**cpf** `string`

**cnpj** `string`

**paginacao[paginaAtual]** `integer`

**paginacao[itensPorPagina]** `string`

Exemplo:

```json
{
  "type": "object",
  "properties": {
    "inicio": {
      "type": "string",
      "format": "date-time",
      "required": true
    },
    "fim": {
      "type": "string",
      "format": "date-time",
      "required": true
    },
    "txid": {
      "type": "string"
    },
    "txIdPresente": {
      "type": "boolean"
    },
    "devolucaoPresente": {
      "type": "boolean"
    },
    "cpf": {
      "type": "string"
    },
    "cnpj": {
      "type": "string"
    },
    "paginacao[paginaAtual]": {
      "type": "integer"
    },
    "paginacao[itensPorPagina]": {
      "type": "string"
    }
  },
  "required": [
    "inicio",
    "fim"
  ]
}
```
<br>

##### **Response**
---

```
200 OK
```

```json
{
  "parametros": {
    "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
    "fim": "2021-02-15T23:55:00Z",
    "inicio": "2021-02-01T19:06:59Z",
    "paginacao": {
      "itensPorPagina": 10,
      "paginaAtual": 1,
      "quantidadeDePaginas": 1,
      "quantidadeTotalDeItens": 1
    }
  },
  "pix": [
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
  ]
}
```

<br>

```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/PixConsultaInvalida",
  "title": "Consulta Pix Inválida",
  "status": 400,
  "detail": "Os parâmetros de consulta à lista de pix recebidos não respeitam o schema ou não fazem sentido semanticamente."
}
```

<br>

```
403 Forbidden
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/AcessoNegado",
  "title": "Acesso Negado",
  "status": 403,
  "detail": "Requisição de participante autenticado que viola alguma regra de autorização."
}
```
