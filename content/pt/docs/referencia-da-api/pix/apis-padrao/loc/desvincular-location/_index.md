---
title: "Criar Location"
linkTitle: "Criar Location"
date: 2022-08-23T15:00:00-03:00
lastmod: 2021-09-19T09:08:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível desvincular as locations.

```
DELETE https://sandbox-api.openbank.stone.com.br/api/v1/loc/{id}/txid
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

**x-stone-idempotency-id*** `string`
<br> Para garantir idempotência das operações.

<br>

##### **BODY PARAMS**
---
<br>

**tipoCob*** `string`
Valores possíveis: `cob` e `cobv`

Exemplo:

```json
{
  "tipoCob": "cob"
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
  "id": 2316,
  "location": "pix.example.com/qr/v2/a8534e273ecb47d3ac30613104544466",
  "tipoCob": "cob",
  "criacao": "2020-05-31T19:39:54.013Z"
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
  "title": "Payload Location Não Encontrado",
  "status": 404,
  "detail": "Entidade não encontrada."
}
```