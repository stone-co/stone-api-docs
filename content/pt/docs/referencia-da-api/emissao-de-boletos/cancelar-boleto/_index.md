---
title: "Cancelar um boleto"
slug: "cancelar-um-boleto"
draft: false
weight: 9

---
---
```http request
POST https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoice/id/cancel
```
---

#### **QUERY PARAMS**
---
<br>

**id*** `string`
<br> Identificador do boleto que se quer cancelar.

<br>


O cancelamento do boleto ocorre de forma assíncrona. Após a solicitação de cancelamento ser efetuada com sucesso, o status será alterado para `cancelation_requested`.

Assim que o processo de cancelamento terminar, o status será alterado para `CANCELLED`. 
<br>Para acompanhar o processo de cancelamento, utilize a api /barcode_payment_invoices/{id}/ e observe o status do boleto.

<br>

{{% pageinfo %}}
**Atenção**

Não será possível cancelar o boleto caso:

- exista algum pagamento em progresso
- o boleto esteja com status `SETTLED`

{{% /pageinfo %}}




<br> 

#### **Response**

```JSON
200 OK
content-type: application/json
```
Body
```JSON

{ }

