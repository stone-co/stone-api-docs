---
title: "Consultar Taxas"
slug: "taxas"
excerpt: "Taxa Cobrada por tipo de Pagamento"
hidden: true
draft: true
date: "2018-10-30T18:52:33.971Z"
lastmod: "2019-12-02T22:56:58.206Z"
---
[block:api-header]
{
  "title": "1. Como consultar Taxas de um Produto"
}
[/block]
Com o intuito de trazer transparência para a cliente, é possível consultar as taxas que ela possui referente a cada produto que utiliza. Por exemplo:

Pagamento de Boleto: `barcode_payment`
Transferência Interna: `internal_transfer`
Transferência Externa: `external_transfer`
[block:callout]
{
  "type": "success",
  "body": "**GET**\n\nhttps://sandbox-api.openbank.stone.com.br/api/v1/accounts/id/fees/fee_type",
  "title": "Para isso, consulte o seguinte endpoint:"
}
[/block]
Antes de realizar o **GET** na requisição, é necessário substituir o {id} da requisição pelo *account_id* da usuária a ser consultada e o tipo de produto que deseja consultar, o `fee_type`.  

Veja o exemplo abaixo, no qual, iremos realizar uma consulta das taxas de pagamento de boleto (`barcode_payment`):

## 1.1 Analisando o JSON

Abaixo temos um JSON da resposta deste comando: 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"amount\": 130\n}",
      "language": "json"
    }
  ]
}
[/block]
Veja que a taxa de pagamento retornou um `amount` de 230, que é referente a R$ 1,30 de taxa de pagamento em reais.
