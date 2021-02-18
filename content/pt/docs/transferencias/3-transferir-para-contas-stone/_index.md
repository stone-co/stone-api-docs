---
title: "Transferir para Contas Stone"
slug: "transferir-para-contas-stone"
draft: false
weight: 3 
createdAt: "2019-04-01T19:18:21.671Z"
updatedAt: "2020-03-02T18:59:37.899Z"
---

Faz transferências monetárias para outra conta dentro da Stone. <br> 

A transferência pode ser agendada, através do campo `scheduled_to`. A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da [API de caléndario de agendamento](https://docs.openbank.stone.com.br/reference#calend%C3%A1rio-de-agendamento) chamada com o parâmetro `operation_type=internal_transfer`. 

Caso a data escolhida seja menor do que `next_available_execution_date`, a transferência será executada imediatamente. <br>
Caso a data seja maior que `execution_limit_date`, será retornado um erro 422. 

A criação e o agendamento de transferências internas pode acontecer em qualquer dia (incluindo fins de semana e feriados) e em qualquer horário.

---
```http request
POST https://sandbox-api.openbank.stone.com.br/api/v1/internal_transfers
content-type: application/json
```
---

#### BODY PARAMS

**amount*** `int32`
<br>Valor da transferência em centavos de Real, ou seja, um real fica 100.

**account_id*** `string`
<br>Identificador da conta que está enviando a transferência.

**target** `object`
	<br>
&nbsp; &nbsp; **account** `object`
		<br>
		 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_code*** `string`
		<br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Número da conta. Padrão: `^\d+$`
	`

##### **Request**
```JSON
{
  "key": “+5510998765432”, 
  "key_type": “phone”, 
  "participant_ispb": “1234567890”,
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "created_at": "2019-11-18T03:00:00Z"
  },
  "beneficiary_entity": {
     "name":"Maria Clara Gomes",
     "document_type": "cpf",
     "document": “13152256685”
  }
}
```

{{% pageinfo %}}
**Ciclo de vida assíncrono** 
<br>

  As transações são executadas de forma assíncrona, então receber o retorno com código 202 não significa que a transação foi executada. É possível enviar uma transação, receber 202 como retorno e logo depois ocorrer uma falha como, por exemplo, saldo insuficiente.
  Também é importante lembrar que a transferência precisa de uma aprovação.
 {{% /pageinfo %}}