---
title: "O Objeto Taxas"
slug: "o-objeto-taxa"
hidden: false
createdAt: "2020-03-04T17:04:54.892Z"
updatedAt: "2020-06-26T01:50:43.062Z"
weight: 10
---


---

### Taxas


<br>

| Chave                                   |    Descrição               | Tipo                               |
| --------------------------------------- | -------------------------  | -----------------------------------|
| amount                                  | Taxa vigente. No caso de external_tranfer pode ser diferente da taxa contratada (original_fee) caso billing_exemption_participant igual a true. | `Integer`
| fee_type                                | Tipo de taxa. Veja abaixo os valores possíveis. | `String`
| billing_exemption_participant           | Só se aplica a external_transfer e barcode_payment_invoice . Indica se a usuária possui alguma condição especial vigente. | `Boolean`
| original_fee                            | Só se aplica a external_transfer e barcode_payment_invoice. Indica a taxa original do item para a essa conta. | `Integer`
| max_free_transfers                      | Só se aplica a external_transfer. Indica o número total de TEDs grátis que a usuária tem no período. | `Integer`
| max_free                                | Só se aplica a barcode_payment_invoice. Indica o número total de boletos gerados que podem ser pagos sem que haja custos no período. | `Integer`
| remaining_free_transfers                | Só se aplica a external_transfer. Indica a número de TEDs grátis restantes no período. | `Integer`
| remaining_free                          | Só se aplica a barcode_payment_invoice. Indica o número restante de boletos gerados que podem ser pagos sem que haja custos no periódo. | `Integer`



{{% pageinfo %}}
**Emissão de boleto**

A cobrança da taxa (barcode_payment_invoice) só é aplicada quando um boleto gerado é pago.
{{% /pageinfo %}}


<br>

### Tipos de taxas


<br>

| Valor                                  |    Descrição                                        |
| -------------------------------------- | --------------------------------------------------  | 
| internal_transfer                      | Tranferência para outra Conta Stone.
| external_transfer                      | Transferência para conta de outra instituição.
| barcode_payment                        | Pagamento de um documento de codigo de barra. (boletos, tributos, concessionárias, etc)
| outbound_stone_prepaid_card_payment    | Compra feita com cartão pré-pago.
| outbound_stone_prepaid_card_withdrawal | Saque feito com cartão.
| barcode_payment_invoice                | Boleto emitido pela Conta Stone que foi pago.





