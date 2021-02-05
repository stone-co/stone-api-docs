---
title: "O Objeto Taxas"
slug: "o-objeto-taxa"
hidden: false
createdAt: "2020-03-04T17:04:54.892Z"
updatedAt: "2020-06-26T01:50:43.062Z"
---
[block:api-header]
{
  "title": "Taxas"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "amount",
    "1-0": "fee_type",
    "2-0": "billing_exemption_participant",
    "3-0": "original_fee",
    "3-1": "Só se aplica a `external_transfer` e `barcode_payment_invoice`. Indica a taxa original do item para a essa conta.",
    "2-1": "Só se aplica a `external_transfer` e `barcode_payment_invoice` . Indica se a usuária possui alguma condição especial vigente.",
    "1-1": "Tipo de taxa. Veja abaixo os valores possíveis.",
    "0-1": "Taxa vigente. No caso de `external_tranfer` pode ser diferente da taxa contratada (`original_fee`) caso `billing_exemption_participant` igual a `true`.",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "2-2": "*Boolean*",
    "3-2": "*Integer*",
    "0-2": "*Integer*",
    "1-2": "*String*",
    "4-0": "max_free_transfers",
    "4-1": "Só se aplica a `external_transfer`. Indica o número total de TEDs grátis que a usuária tem no período.",
    "6-0": "remaining_free_transfers",
    "6-1": "Só se aplica a `external_transfer`. Indica a número de TEDs grátis restantes no período.",
    "4-2": "*Integer*",
    "6-2": "*Integer*",
    "5-0": "max_free",
    "5-1": "Só se aplica a `barcode_payment_invoice`. Indica o número total de boletos gerados que podem ser pagos sem que haja custos no período.",
    "5-2": "*Integer*",
    "7-0": "remaining_free",
    "7-1": "Só se aplica a `barcode_payment_invoice`. \nIndica o número restante de boletos gerados que podem ser pagos sem que haja custos no periódo.",
    "7-2": "*Integer*"
  },
  "cols": 3,
  "rows": 8
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Emissão de boleto",
  "body": "A cobrança da taxa (barcode_payment_invoice) só é aplicada quando um boleto gerado é pago."
}
[/block]

[block:api-header]
{
  "title": "Tipos de taxas"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Valor",
    "h-1": "Descrição",
    "0-0": "`internal_transfer`",
    "1-0": "`external_transfer`",
    "2-0": "`barcode_payment`",
    "3-0": "`outbound_stone_prepaid_card_payment`",
    "4-0": "`outbound_stone_prepaid_card_withdrawal`",
    "5-0": "`barcode_payment_invoice`",
    "0-1": "Tranferência para outra Conta Stone.",
    "1-1": "Transferência para conta de outra instituição.",
    "2-1": "Pagamento de um documento de codigo de barra. (boletos, tributos, concessionárias, etc)",
    "3-1": "Compra feita com cartão pré-pago.",
    "4-1": "Saque feito com cartão.",
    "5-1": "Boleto emitido pela Conta Stone que foi pago."
  },
  "cols": 2,
  "rows": 6
}
[/block]