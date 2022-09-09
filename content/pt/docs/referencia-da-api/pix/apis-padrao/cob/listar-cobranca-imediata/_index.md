---
title: "Listar Cobrança imediata"
linkTitle: "Listar Cobrança imediata"
date: 2022-08-23T15:00:00-03:00
lastmod: 2022-08-23T15:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível listar as cobranças imediatas por Pix.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/cob/
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

```
200 OK
```

```json
{
	"parametros": {
		"inicio": "2020-04-01T00:00:00Z",
		"fim": "2020-04-02T10:00:00Z",
		"paginacao": {
			"paginaAtual": 0,
			"itensPorPagina": 100,
			"quantidadeDePaginas": 1,
			"quantidadeTotalDeItens": 2
		}
	},
	"cobs": [{
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
		"infoAdicionais": [{
				"nome": "Campo 1",
				"valor": "Informação Adicional1 do PSP-Recebedor"
			},
			{
				"nome": "Campo 2",
				"valor": "Informação Adicional2 do PSP-Recebedor"
			}
		]
	}]
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
    "propriedade": "cpf",
    "razao": "Não respeita o schema",
    "valor": "123"
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
