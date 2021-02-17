---
title: "Criar Um Pagamento"
slug: "criar-um-pagamento"
hidden: false
createdAt: "2019-06-04T19:16:40.905Z"
updatedAt: "2020-04-28T15:16:04.117Z"
weight: 3
description: >
---

Usado para realizar pagamentos de boleto e concessionárias.

---
<br>

{{% pageinfo %}}
**Atenção**

O pagamento pode ser agendado através do campo `scheduled_to`. 

A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da API de calendário de agendamento chamada com o parâmetro `operation_type=payment`. 

Caso a data escolhida seja menor do que `next_available_execution_date`, o pagamento será executado imediatamente. 

Caso a data seja maior que `execution_limit_date`, será retornado um erro 422 na criação. 

A criação e o agendamento de pagamentos pode acontecer em qualquer dia (incluindo fins de semana e feriados) e em qualquer horário.

{{% /pageinfo %}}


<br>

---


```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/payments
```

---

**BODY PARAMS**

---

**barcode***  `string` 

Código de barras do documento.

<br>

---

**account_id***  `string` 

Identificador da conta que irá pagar o documento.

<br>

---

**scheduled_to***  `string` 

Formato: `yyyy-mm-dd`

<br>

---

**HEADERS**

---

**x-stone-idempotency-key***  `string`

Chave de idempotencia.


<br>
---

##### **Response**

```JSON
202 Accepted 
```

```JSON
{
    "account_id": "8cbeb3d2-750f-4b14-81a1-143ad715c273",
    "amount": 100,
    "approval_expired_at": null,
    "approved_at": "2019-08-02T18:22:19Z",
    "approved_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "barcode": "89670000000010003137498189637166095077491613",
    "cancelled_at": null,
    "created_at": "2019-08-02T18:22:19Z",
    "created_by": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "details": null,
    "failed_at": null,
    "failure_reason_code": null,
    "failure_reason_description": null,
    "fee": 0,
    "finished_at": null,
    "id": "1879158c-03c6-48ff-b7c3-c34a992cfa9c",
    "refunded_at": null,
    "rejected_at": null,
    "rejected_by": null,
    "scheduled_to": null,
    "status": "APPROVED",
    "writable_line": "896700000004010003137493818963716605950774916130"
}
```