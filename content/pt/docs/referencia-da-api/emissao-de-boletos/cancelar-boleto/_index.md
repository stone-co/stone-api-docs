---
title: "Cancelar um boleto"
slug: "cancelar-um-boleto"
draft: false
weight: 9

---
---

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

- **Baixa Manual de Boletos**
	
	A API para baixa manual de boletos e concessionárias fica disponível 24/7;

	Baixa de boletos realizadas após às 23h50 ocorrerão no dia útil seguinte em que a operação foi realizada; 
	
	Baixa manual de concessionárias são realizadas entre 7h00 e 20h00, ou seja, baixas solicitadas após às 20h serão realizadas às 7h do dia seguinte.

<br>

{{< /alert >}}

<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/barcode_payment_invoices/id/cancel
```
<br>

#### **QUERY PARAMS**
---
<br>

**id*** `string`
<br> Identificador do boleto que se quer cancelar.

<br>


O cancelamento do boleto ocorre de forma assíncrona. Após a solicitação de cancelamento ser efetuada com sucesso, o status será alterado para `CANCELLATION_REQUESTED`.

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

```
200 OK
content-type: application/json
```
Body
```json

{ }

