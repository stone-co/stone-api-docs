---
title: "Recuperar Location"
linkTitle: "Recuperar Location"
date: 2022-08-23T15:00:00-03:00
lastmod: 2022-08-23T15:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível recuperar as locations.

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/loc/{id}
```
<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.


##### **PATH PARAMS**
---
<br>

**id*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"

<br>

##### **Response**
---

```
200 OK
```

```json
{
  "id": 7716,
  "txid": "fda9460fe04e4f129b72863ae57ee22f",
  "location": "pix.example.com/qr/v2/cobv/2353c790eefb11eaadc10242ac120002",
  "tipoCob": "cobv",
  "criacao": "2020-03-11T21:19:51.013Z"
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