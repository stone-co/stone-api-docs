---
title: "Listar QRCode Dinâmico com Validade"
linkTitle: "Listar QRCode Dinâmico com Validade"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-09-19T09:08:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível revisar as cobranças com validade por Pix.


```
PATCH https://sandbox-api.openbank.stone.com.br/api/v1/cobv/{txid}
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

**calendario*** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**dataDeVencimento*** `date`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**validadeAposVencimento** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Quantidade de dias corridos após calendario.dataDeVencimento em que a cobrança poderá ser paga

**loc** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**id** `integer`

**status** `string`
Valores possíveis: `REMOVIDA_PELO_USUARIO_RECEBEDOR`

**devedor** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**logradouro** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**cidade** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**uf** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**cep** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**cpf** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**nome** `string`

**valor** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**original*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;Valor original da cobrança. Ex: 123,34
<br>&nbsp;&nbsp;&nbsp;&nbsp;**abatimento** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fixo: 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual: 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;**multa** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fixo: 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual: 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;**juros** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor (dias corridos): 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao dia (dias corridos): 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao mês (dias corridos): 3
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao ano (dias corridos): 4
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor (dias úteis): 5
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao dia (dias úteis): 6
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao mês (dias úteis): 7
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao ano (dias úteis): 8       
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;**desconto** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor Fixo até a[s] data[s] informada[s]: 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual até a data informada: 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor por antecipação dia corrido: 3
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor por antecipação dia útil: 4
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual por antecipação dia corrido: 5
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual por antecipação dia útil: 6
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Obrigatório para modalidades 3 a 6
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**descontoDataFixa** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Obrigatório para modalidades 1 a 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**data*** `date`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}

**chave*** `string`
<br>Chave Pix do dono da conta

**solicitacaoPagador** `string`
<br>Solicitação ao pagador - campo de texto livre

**infoAdicionais** `list` of `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**nome** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;**valor** `string`


Exemplo de Body:

```json
{
  "loc": {
    "id": 789
  },
  "devedor": {
    "logradouro": "Alameda Souza, Numero 80, Bairro Braz",
    "cidade": "Recife",
    "uf": "PE",
    "cep": "70011750",
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
200 OK
```

```json
{
	"calendario": {
		"criacao": "2020-09-09T20:15:00.358Z",
		"dataDeVencimento": "2020-12-31",
		"validadeAposVencimento": 30
	},
	"txid": "7978c0c97ea847e78e8849634473c1f1",
	"revisao": 0,
	"loc": {
		"id": 789,
		"location": "pix.example.com/qr/c2/cobv/9d36b84fc70b478fb95c12729b90ca25",
		"tipoCob": "cobv"
	},
	"status": "ATIVA",
	"devedor": {
		"logradouro": "Alameda Souza, Numero 80, Bairro Braz",
		"cidade": "Recife",
		"uf": "PE",
		"cep": "70011750",
		"cpf": "12345678909",
		"nome": "Francisco da Silva"
	},
	"recebedor": {
		"logradouro": "Rua 15 Numero 1200, Bairro São Luiz",
		"cidade": "São Paulo",
		"uf": "SP",
		"cep": "70800100",
		"cnpj": "56989000019533",
		"nome": "Empresa de Logística SA"
	},
	"valor": {
		"original": "123.45"
	},
	"chave": "5f84a4c5-c5cb-4599-9f13-7eb4d419dacc",
	"solicitacaoPagador": "Cobrança dos serviços prestados."
}
```

```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/CobVOperacaoInvalida",
  "title": "Cobrança inválida.",
  "status": 400,
  "detail": "A requisição que busca alterar ou criar uma cobrança com vencimento não respeita o schema ou está semanticamente errada",
  "violacoes": {
    "propriedade": "original",
    "razao": "tem seu formato inválido",
    "valor": "@@@"
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