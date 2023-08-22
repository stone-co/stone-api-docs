---
title: "Revisar Cobrança imediata"
linkTitle: "Revisar Cobrança imediata"
date: 2022-08-23T15:00:00-03:00
lastmod: 2022-08-23T15:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível revisar as cobranças imediatas por Pix.


```
PATCH https://sandbox-api.openbank.stone.com.br/api/v1/cob/{txid}
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

##### **PATH PARAMS**
---
<br>

**txid*** `string`
<br>Validação: "^[a-zA-Z0-9]{26,35}$"

<br>

##### **BODY PARAMS**
---
<br>

**calendario** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**expiracao*** `date`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Tempo de vida da cobrança em segundos. O padrão é `86400`

**loc** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**id** `integer`

**devedor** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**cpf** ou `cnpj` `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**nome** `string`

**valor** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**original*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valor original da cobrança. Ex: 123,34

**chave** `string`
<br>Chave Pix do dono da conta

**solicitacaoPagador** `string`
<br>Solicitação ao pagador - campo de texto livre

**infoAdicionais** `list` of `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**nome** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**valor** `string`


Exemplo:

```json
{
  "loc": {
    "id": 7768
  },
  "devedor": {
    "cpf": "12345678909",
    "nome": "Francisco da Silva"
  },
  "valor": {
    "original": "123.45"
  },
  "solicitacaoPagador": "Cobrança dos serviços prestados."
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
  "calendario": {
    "criacao": "2020-09-09T20:15:00.358Z",
    "expiracao": 3600
  },
  "txid": "7978c0c97ea847e78e8849634473c1f1",
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
  "infoAdicionais": [
    {
      "nome": "Campo 1",
      "valor": "Informação Adicional1 do PSP-Recebedor"
    },
    {
      "nome": "Campo 2",
      "valor": "Informação Adicional2 do PSP-Recebedor"
    }
  ],
  "qr_code_copia_cola": "<string>",
  "qr_code": "<string>"
}
```

```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/CobOperacaoInvalida",
  "title": "Cobrança inválida.",
  "status": 400,
  "detail": "A requisição que busca alterar ou criar uma cobrança para pagamento imediato não respeita o schema ou está semanticamente errada.",
  "violacoes": {
    "propriedade": "devedor.cpf ou devedor.cnpj",
    "razao": "deve ser preenchido"
  }
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
