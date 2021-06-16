---
title: "Consultar Pix recebido por QRCode"
linkTitle: "Consultar Pix recebido por QRCode"
date: 2021-06-16T15:17:00-03:00
lastmod: 2021-06-16T15:17:00-03:00
weight: 4
description: >
  
---

Através desse endpoint será possível consultar QRCodes com vencimento e valores monetários calculados. Segue padrões definidos pelo BACEN.


```http request
GET https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{id}}
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

**id*** `string`
<br> ID da cobrança com vencimento.

<br>

##### **QUERY PARAMS**
---
<br>

**dpp** `string`
<br> Data de pagamento pretendida.

**codMun** `string`
<br> Código IBGE do município.


<br>

##### **Response**
---

```JSON
200 OK
```

```JSON
{
  "calendario": {
    "apresentacao": "2021-03-26T20:35:33Z",
    "criacao": "2021-03-26T20:26:49Z",
    "dataDeVencimento": "2021-03-27",
    "validadeAposVencimento": 15
  },
  "chave": "4e4bb64d-d17c-4c53-a51b-44f06e28be06",
  "devedor": {
    "nome": "Fulano da Silva",
    "cpf": "85553990335"
  },
  "infoAdicionais": [
    {
      "nome": "Mr. Due",
      "valor": "Date Three"
    }
  ],
  "recebedor": {
    "cep": "22250120",
    "cidade": "Rio de JaneiroA",
    "cpf": "91092573062",
    "logradouro": "Rua Honório de BarrosoA, Número 3A, Bairro FlamengoA",
    "nome": "Gilderoy Lockhart",
    "nomeFantasia": null,
    "uf": "RJA"
  },
  "revisao": 0,
  "solicitacaoPagador": null,
  "status": "ATIVA",
  "txid": "a2f6db6e14844c55bc02a5c1a78b0eea",
  "valor": {
    "abatimento": "1.00",
    "final": "19.00",
    "original": "20.00"
  }
}
```

---

```JSON
400 Bad Request
```

```JSON
{
  "type": "https://pix.bcb.gov.br/api/v2/error/PixConsultaInvalida",
  "title": "Consulta Pix Inválida",
  "status": 400,
  "detail": "Os parâmetros de consulta à lista de pix recebidos não respeitam o schema ou não fazem sentido semanticamente."
}
```

---

```JSON
404 Not found
```

```JSON
{
  "type": "https://pix.bcb.gov.br/api/v2/error/PixNaoEncontrado",
  "title": "Não Encontrado",
  "status": 404,
  "detail": "Entidade não encontrada."
}
