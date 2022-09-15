---
title: "Detalhes Cobrança imediata"
linkTitle: "Detalhes Cobrança imediata"
date: 2022-08-23T15:00:00-03:00
lastmod: 2022-08-23T15:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível possível consultar as cobranças imediatas por Pix.

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/cob/{txid}
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

**txid*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"
<br>


##### **Response**
---

```
200 OK
```

```json
{
    "calendario": {
        "criacao": "2020-09-09T20:15:00.358Z",
        "expiracao": 3600
    },
    "txid": "7978   c0c97ea847e78e8849634473c1f1",
    "revisao": 0,
    "loc": {
        "id": 789,
        "location": "pix.example.com/qr/9d36b84fc70b478fb95c12729b90ca25",
        "tipoCob": "cob"
    },
    "location": "pix.example.com/qr/9d36b84fc70b478fb95c12729b90ca25",
    "status": "ATIVA",
    "devedor": {
        "cnpj": "12345678000195",
        "nome": "Empresa de Serviços SA"
    },
    "valor": {
        "original": "37.00",
        "modalidadeAlteracao": 1
    },
    "chave": "7d9f0335-8dcc-4054-9bf9-0dbd61d36906",
    "solicitacaoPagador": "Serviço realizado.",
    "infoAdicionais": [{
            "nome": "Campo 1",
            "valor": "Informação Adicional1 do PSP-Recebedor"
        },
        {
            "nome": "Campo 2",
            "valor": "Informação Adicional2 do PSP-Recebedor"
        }
    ]
}

```

```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/CobOperacaoInvalida",
  "title": "Cabeçalho inválida.",
  "status": 400,
  "detail": "O cabeçalho x-stone-account-id deve ser preenchido com um valor válido."
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