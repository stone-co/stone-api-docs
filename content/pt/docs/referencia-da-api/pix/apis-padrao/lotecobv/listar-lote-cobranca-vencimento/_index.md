---
title: "Listar Lote Cobranças Vencimento"
linkTitle: Listar Lote Cobranças Vencimento"
date: 2022-08-23T20:00:00-03:00
lastmod: 2022-08-23T20:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível listar lotes de cobranças com vencimento por Pix.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/lotecobv
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

```
200 OK
```

```json
{
  "parametros": {
    "inicio": "2020-01-01T00:00:00Z",
    "fim": "2020-12-01T23:59:59Z",
    "paginacao": {
      "paginaAtual": 0,
      "itensPorPagina": 100,
      "quantidadeDePaginas": 1,
      "quantidadeTotalDeItens": 2
    }
  },
  "lotes": [
    {
        "descricao": "Cobranças dos alunos do turno vespertino",
        "criacao": "2020-11-01T20:15:00.358Z",
        "cobsv": [
            {
            "criacao": "2020-11-01T20:15:00.358Z",
            "txid": "fb2761260e554ad593c7226beb5cb650",
            "status": "CRIADA"
            },
            {
            "txid": "7978c0c97ea847e78e8849634473c1f1",
            "status": "NEGADA",
            "problema": {
                "type": "https://pix.bcb.gov.br/api/v2/error/CobVOperacaoInvalida",
                "title": "Cobrança inválida.",
                "status": 400,
                "detail": "A requisição que busca alterar ou criar uma cobrança com vencimento não respeita o _schema_ ou está semanticamente errada.",
                "violacoes": [
                {
                    "razao": "O objeto cobv.devedor não respeita o _schema_.",
                    "propriedade": "cobv.devedor"
                }
                ]
            }
            }
        ]
    }

  ]
}
```

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

```
404 Not Found
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/NaoEncontrado",
  "title": "Não Encontrado",
  "status": 404,
  "detail": "Entidade não encontrada."
}
```