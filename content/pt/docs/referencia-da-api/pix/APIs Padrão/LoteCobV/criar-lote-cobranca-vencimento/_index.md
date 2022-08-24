---
title: "Criar Lote Cobranças Vencimento"
linkTitle: Criar Lote Cobranças Vencimento"
date: 2022-08-23T20:00:00-03:00
lastmod: 2022-08-23T20:00:00-03:00
weight: 8
description: >
  
---

Através desse endpoint será possível criar lote de cobranças com vencimento por Pix.


```
PUT https://sandbox-api.openbank.stone.com.br/api/v1/lotecobv/{id}
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

**id*** `string`

<br>

##### **BODY PARAMS**
---
<br>

<br> &nbsp;&nbsp;&nbsp;&nbsp;**txid** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Format: "^[a-zA-Z0-9]{26,35}$"

<br> &nbsp;&nbsp;&nbsp;&nbsp;**calendario*** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**dataDeVencimento*** `date`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**validadeAposVencimento** `integer`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Quantidade de dias corridos após calendario.dataDeVencimento em que a cobrança poderá ser paga

<br> &nbsp;&nbsp;&nbsp;&nbsp;**loc** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**id** `integer`

<br> &nbsp;&nbsp;&nbsp;&nbsp;**devedor*** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**logradouro** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**cidade** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**uf** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**cep** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**cpf** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**nome** `string`

<br> &nbsp;&nbsp;&nbsp;&nbsp;**valor*** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**original*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor original da cobrança. Ex: 123,34
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**abatimento** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fixo: 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual: 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**multa** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fixo: 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual: 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**juros** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor (dias corridos): 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao dia (dias corridos): 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao mês (dias corridos): 3
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao ano (dias corridos): 4
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor (dias úteis): 5
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao dia (dias úteis): 6
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao mês (dias úteis): 7
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual ao ano (dias úteis): 8       
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**desconto** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**modalidade*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valores permitidos:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor Fixo até a[s] data[s] informada[s]: 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual até a data informada: 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor por antecipação dia corrido: 3
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valor por antecipação dia útil: 4
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual por antecipação dia corrido: 5
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentual por antecipação dia útil: 6
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Obrigatório para modalidades 3 a 6
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**descontoDataFixa** `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Obrigatório para modalidades 1 a 2
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**data*** `date`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valorPerc*** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Format: \d{1,10}\.\d{2}

<br>&nbsp;&nbsp;&nbsp;&nbsp;**chave*** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Chave Pix do dono da conta

<br>&nbsp;&nbsp;&nbsp;&nbsp;**solicitacaoPagador** `string`
<br> &nbsp;&nbsp;&nbsp;&nbsp;Solicitação ao pagador - campo de texto livre

<br>&nbsp;&nbsp;&nbsp;&nbsp;**infoAdicionais** `list` of `object`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**nome** `string`
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**valor** `string`


Exemplo:

```json
{
  "descricao": "Cobranças dos alunos do turno vespertino",
  "cobsv": [
    {
      "calendario": {
        "dataDeVencimento": "2020-12-31",
        "validadeAposVencimento": 30
      },
      "txid": "fb2761260e554ad593c7226beb5cb650",
      "loc": {
        "id": 789
      },
      "devedor": {
        "logradouro": "Alameda Souza, Numero 80, Bairro Braz",
        "cidade": "Recife",
        "uf": "PE",
        "cep": "70011750",
        "cpf": "08577095428",
        "nome": "João Souza"
      },
      "valor": {
        "original": "100.00"
      },
      "chave": "7c084cd4-54af-4172-a516-a7d1a12b75cc",
      "solicitacaoPagador": "Informar matrícula"
    },
    {
      "calendario": {
        "dataDeVencimento": "2020-12-31",
        "validadeAposVencimento": 30
      },
      "txid": "7978c0c97ea847e78e8849634473c1f1",
      "loc": {
        "id": 57221
      },
      "devedor": {
        "logradouro": "Rua 15, Numero 1, Bairro Campo Grande",
        "cidade": "Recife",
        "uf": "PE",
        "cep": "70055751",
        "cpf": "15311295449",
        "nome": "Manoel Silva"
      },
      "valor": {
        "original": "100.00"
      },
      "chave": "7c084cd4-54af-4172-a516-a7d1a12b75cc",
      "solicitacaoPagador": "Informar matrícula"
    }
  ]
}

```
<br>

##### **Response**
---

```
202 OK
```

```json
{
    "message": "Solicitação de revisão do Lote de cobranças encaminhada para processamento."
}
```


```
400 Bad Request
```

```json
{
  "type": "https://pix.bcb.gov.br/api/v2/error/LoteCobVOperacaoInvalida",
  "title": "Cobrança inválida.",
  "status": 400,
  "detail": "A requisição que busca alterar ou criar um lote de cobranças com vencimento não respeita o schema ou está semanticamente errada.",
  "violacoes": {
    "propriedade": "id",
    "razao": "não respeita o schema"
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
