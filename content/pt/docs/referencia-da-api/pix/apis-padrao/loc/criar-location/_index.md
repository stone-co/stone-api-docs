---
title: "Criar Location"
linkTitle: "Criar Location"
date: 2022-08-23T15:00:00-03:00
lastmod: 2022-08-23T15:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível criar as locations.


```
POST https://sandbox-api.openbank.stone.com.br/api/v1/loc
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
201 OK
```

```json
{
  "id": 7716,
  "location": "pix.example.com/qr/v2/2353c790eefb11eaadc10242ac120002",
  "tipoCob": "cob",
  "criacao": "2020-03-11T21:19:51.013Z"
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