---
title: "Detalhes Cobrança com Vencimento"
linkTitle: "Detalhes Cobrança com Vencimento"
date: 2022-08-23T00:17:00-03:00
lastmod: 2022-08-23T00:08:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível detalhar uma cobrança com vencimento por Pix.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/cobv/{txid}
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
<br>Identificador do QR code dinâmico com data de vencimento
<br>


##### **Response**
---

```
201 OK
```

```json
{
  "calendario": {
    "dataDeVencimento": "2020-12-31",
    "validadeAposVencimento": 30
  },
  "loc": {
    "id": 789
  },
  "devedor": {
    "cpf": "12345678909",
    "nome": "Francisco da Silva"
  },
  "valor": {
    "original": "123.45",
    "multa": {
      "modalidade": "2",
      "valorPerc": "15.00"
    },
    "juros": {
      "modalidade": "2",
      "valorPerc": "2.00"
    },
    "desconto": {
      "modalidade": "1",
      "descontoDataFixa": [
        {
          "data": "2020-11-30",
          "valorPerc": "30.00"
        }
      ]
    }
  },
  "chave": "5f84a4c5-c5cb-4599-9f13-7eb4d419dacc",
  "solicitacaoPagador": "Cobrança dos serviços prestados."
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