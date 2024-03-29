---
title: "Transferir para Contas Stone"
slug: "transferir-para-contas-stone"
draft: false
weight: 3 
date: "2019-04-01T19:18:21.671Z"
lastmod: "2020-03-02T18:59:37.899Z"
---

---
<br>

Faz transferências monetárias para outra conta dentro da Stone. <br> 

<br>

A transferência pode ser agendada, através do campo `scheduled_to`. A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da [API de caléndario de agendamento](/docs/referencia-da-api/agendamento/calendario-de-agendamento/) chamada com o parâmetro `operation_type=internal_transfer`. 

Caso a data escolhida seja menor do que `next_available_execution_date`, a transferência será executada imediatamente. <br>
Caso a data seja maior que `execution_limit_date`, será retornado um erro 422. 

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A criação e o agendamento de transferências internas pode acontecer em qualquer dia (incluindo fins de semana e feriados) e em qualquer horário.
{{< /alert >}}

<br>


---
```
POST https://sandbox-api.openbank.stone.com.br/api/v1/internal_transfers
```
---

#### **BODY PARAMS**
---
<br>

**amount*** `int32`
<br>Valor da transferência em centavos de Real, ou seja, um real fica 100.

---
<br>

**account_id*** `string`
<br>Identificador da conta que está enviando a transferência.

---
<br>

**target** `object`
	<br>
&nbsp; &nbsp; **account** `object`
		<br>
		 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**account_code*** `string`
		<br>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Número da conta. Padrão: `^\d+$`
	
---
<br>

**description** `string`
<br>Descrição da transação. Essa descrição será exibida tanto no extrato de quem enviou quanto de quem recebeu (limite 200 caracteres).

---
<br>

**scheduled_to** `string`
<br>Formato: `yyyy-mm-dd`

<br>

#### **HEADERS**
---
<br>

**x-stone-idempotency-key** `string`
<br>Chave de idempotência

<br>As transferências internas estão disponíveis 24hs por dia. Elas se referem a transações entre contas Stone.


{{% pageinfo %}}
**Ciclo de vida assíncrono** 
<br>

  As transações são executadas de forma assíncrona, então receber o retorno com código 202 não significa que a transação foi executada. É possível enviar uma transação, receber 202 como retorno e logo depois ocorrer uma falha como, por exemplo, saldo insuficiente.
  Também é importante lembrar que a transferência precisa de uma aprovação.
 {{% /pageinfo %}}
 
 

<br>

##### **Response**

```
202 Accepted
content-type: application/json
```
Body
```json

{
    "amount": 100,
    "approval_expired_at": null,
    "approved_at": "2019-08-02T18:00:27Z",
    "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "cancelled_at": null,
    "created_at": "2019-08-02T18:00:27Z",
    "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "description": "",
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "finished_at": null,
    "id": "c97de6a6-a35a-423d-a3df-add006a0038e",
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to": null,
    "settled_at": null,
    "status": "APPROVED",
    "target": {
        "account": {
            "account_code": "58859"
        },
        "entity": {
            "name": "Fernando Antonio"
        }
    },
    "target_account_code": "58859",
    "target_account_owner_name": "Fernando Antonio"
}
