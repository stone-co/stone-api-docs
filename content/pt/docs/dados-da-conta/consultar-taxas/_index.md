---
title: "Consultar Taxas"
slug: "consultar-taxas"
hidden: false
createdAt: "2019-04-01T19:09:32.363Z"
updatedAt: "2020-03-30T14:45:05.877Z"
---
Veja que a taxa de pagamento retornou um `amount` de 130, que é referente a R$ 1,30 de taxa de pagamento em reais.
[block:callout]
{
  "type": "danger",
  "title": "Outros campos",
  "body": "No caso de `external_transfer` serão também retornados os campos `billing_exempition_participant`,  `original_fee`, `max_free_transfers` e `remaining_free_transfers`.\n\nNo caso de `barcode_payment_invoice` também serão retornardos os campos `billing_exempition_participant`,  `original_fee`, `max_free`  e `remaining_free` ."
}
[/block]