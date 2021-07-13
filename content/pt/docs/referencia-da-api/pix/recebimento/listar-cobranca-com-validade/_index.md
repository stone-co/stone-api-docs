---
title: "Listar Cobranças com Validade"
linkTitle: "Listar Cobranças com Validade"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-06-16T15:17:00-03:00
weight: 4
description: >
  
---

Através desse endpoint será possível listar as cobranças com validade por Pix.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/cobv
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

**cpf** `string`

**cnpj** `string`

**status** `string`
<br> Possíveis valores: ATIVA, CONCLUIDA, REMOVIDA_PELO_USUARIO_RECEBEDOR, REMOVIDA_PELO_PSP

**paginacao[paginaAtual]** `integer`

**paginacao[itensPorPagina]** `integer`

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
    "cpf": {
      "type": "string"
    },
    "cnpj": {
      "type": "string"
    },
    "status": {
      "type": "string",
      "description": "Possíveis valores: ATIVA, CONCLUIDA, REMOVIDA_PELO_USUARIO_RECEBEDOR, REMOVIDA_PELO_PSP"
    },
    "paginacao[itensPorPagina]": {
      "type": "integer"
    },
    "paginacao[paginaAtual]": {
      "type": "integer"
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

```JSON
200 OK
```

```JSON
    {
      "calendario": {
        "criacao": "2021-03-19T22:04:24.209571Z",
        "dataDeVencimento": "2021-03-18",
        "validadeAposVencimento": 0
      },
      "chave": "4e4bb64d-d17c-4c53-a51b-44p06e28be06",
      "devedor": {
        "nome": "Fulano da Silva",
        "cpf": "85553990335"
      },
      "infoAdicionais": [
        {
          "nome": "Mr. Due",
          "valor": "Date Three"
        }
      ],
      "loc": {
        "criacao": "2021-03-19T22:04:24.209571Z",
        "id": "5672cf6b-7021-4bce-b809-ed2e2d34e888",
        "location": "pix-h.stone.com.br/pix/v2/5672cf6b-7021-4bce-b809-ed2e2d34e888",
        "tipoCob": "cobv"
      },
      "recebedor": {
        "cep": "22250190",
        "cidade": "Rio de Janeiro",
        "logradouro": "Rua Honório de BarrosoA, 3A, FlamengoA",
        "nome": "Gilderoy Lockhart",
        "uf": "RJA",
        "cpf": "91092575062"
      },
      "revisao": 1,
      "solicitacaoPagador": "do something until today",
      "status": "REMOVIDA_PELO_USUARIO_RECEBEDOR",
      "txid": "6225a6024fd242e7b5d2c00a9dc62238",
      "valor": {
        "abatimento": {
          "modalidade": 1,
          "valorPerc": "0.50"
        },
        "desconto": {
          "modalidade": 4,
          "valorPerc": "0.60"
        },
        "juros": {
          "modalidade": 5,
          "valorPerc": "0.50"
        },
        "multa": {
          "modalidade": 1,
          "valorPerc": "90.90"
        },
        "original": "5.55"
      }
    }
```