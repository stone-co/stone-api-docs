---
title: "Listar Cobrança com Vencimento"
linkTitle: "Listar Cobrança com Vencimento"
date: 2022-07-23T15:17:00-03:00
lastmod: 2022-07-23T15:17:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível listar as cobranças com vencimento por Pix.


```
GET https://sandbox-api.openbank.stone.com.br/api/v1/cobv
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
  		"fim": "2020-04-01T23:59:59Z",
  		"paginacao": {
  			"paginaAtual": 0,
  			"itensPorPagina": 100,
  			"quantidadeDePaginas": 1,
  			"quantidadeTotalDeItens": 1
  		}
  	},
  	"cobs": [{
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
  				"descontoDataFixa": [{
  					"data": "2020-11-30",
  					"valorPerc": "30.00"
  				}]
  			}
  		},
  		"chave": "5f84a4c5-c5cb-4599-9f13-7eb4d419dacc",
  		"solicitacaoPagador": "Cobrança dos serviços prestados."
  	}]
  }
```
