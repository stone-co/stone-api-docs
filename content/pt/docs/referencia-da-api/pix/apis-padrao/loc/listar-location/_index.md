---
title: "Criar Location"
linkTitle: "Criar Location"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-09-19T09:08:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível criar as locations.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/loc
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **Response**
---

```
200 OK
```

```json

  "parametros": {
    "inicio": "2020-04-01T00:00:00Z",
    "fim": "2020-04-01T23:59:59Z",
    "paginacao": {
      "paginaAtual": 0,
      "itensPorPagina": 100,
      "quantidadeDePaginas": 1,
      "quantidadeTotalDeItens": 3
    }
  },
  "loc": [
    {
    "id": 7716,
    "txid": "fda9460fe04e4f129b72863ae57ee22f",
    "location": "pix.example.com/qr/v2/cobv/2353c790eefb11eaadc10242ac120002",
    "tipoCob": "cobv",
    "criacao": "2022-03-11T21:19:51.013Z"
    }
  ]
}
```

```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/PayloadLocationOperacaoInvalida",
  "title": "PayloadLocation inválido.",
  "status": 400,
  "detail": "A presente requisição busca criar uma location sem respeitar o schema estabelecido."
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
