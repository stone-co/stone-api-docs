---
title: "Criar devolução para Pix recebido"
linkTitle: "Criar devolução para Pix recebido"
date: 2022-08-17T00:00:00-03:00
lastmod: 2022-08-17T00:00:00-03:00
weight: 9
description: >
  
---

Através desse endpoint será possível criar uma devolução para um Pix recebido utilizando o indentificador global (EndToEndId) de uma transação Pix recebida. 

```
PUT https://sandbox-api.openbank.stone.com.br/api/v1/pix/{e2eid}/devolucao/{id}
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

**id*** `string`
<br> Identificador do pagamento.

<br>Format: [a-zA-Z0-9]{1,35}


##### **BODY PARAMS**
---

**valor***  `string`
<br> Valor a ser devolvido. Deve ser igual ou inferior ao valor da transação original.
<br> Format: \d{1,10}\.\d{2}

Exemplo body:

```json
{
  "valor": "7.89"
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
  "id": "123456",
  "rtrId": "D12345678202009091000abcde123456",
  "valor": "7.89",
  "horario": {
    "solicitacao": "2020-09-11T15:25:59.411Z"
  },
  "status": "EM_PROCESSAMENTO"
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
  "detail": "Os parâmetros de consulta à lista de pix recebidos não respeitam o schema ou não fazem sentido semanticamente.",
  "violacoes": [{
    "propriedade": "valor",
    "razao": "tem seu formato inválido",
    "valor": "invalid"
  },
  {
    "propriedade": "id",
    "razao": "tem seu formato inválido",
    "valor": "@@@@"
  }]
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
