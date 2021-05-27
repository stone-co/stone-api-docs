---
title: "Criar pagamento de folha"
slug: "criar-pagamento-de-folha"
draft: false
weight: 2
date: "2019-09-12T17:15:41.268Z"
lastmod: "2019-09-30T17:25:00.496Z"
---
---

{{< alert title="Horário de funcionamento" >}}
<br>

A API de Folha de Pagamentos funciona em dias úteis, 24 horas por dia, ou seja, o salário é depositado no mesmo momento do pagamento.

Para usuários com portabilidade de salário ativa, o salario só estará disponível na conta caso pago em dias úteis das 06h30 às 16h00, caso contrario o salario ficará disponível no próximo dia útil às 09h00. 

{{< /alert >}}


<br>


```http 
POST https://sandbox-api.openbank.stone.com.br/api/v1/payrolls
```
---

#### **BODY PARAMS**

---
**account_id***  `string`
<br> Identificador da conta no formato UUID.

---
**salaries_id***  `string`
<br> Identificador de salário no formato UUID.

{{% pageinfo %}}
**salaries_id**
<br>Esse parâmetro é o identificador de um arquivo contendo os salários, o qual é enviado através do endpoint https://sandbox-payroll.openbank.stone.com.br/api/payroll/upload.
<br>O arquivo deverá ser enviado a este endpoint, retornando um id, esse id será o `salaries_id` a ser utilizado para criar um pagamento de folha.
<br>O arquivo é uma planilha (.xlsx) com as seguintes colunas: Nome, CPF, Conta (número da conta na Stone) e Salário.
{{% /pageinfo %}}

<br>

#### **Response**

```JSON
202 Accepted
content-type: application/json
```
Body
```JSON
{
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "amount": 100,
  "created_at": "2019-09-11T10:14:08Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "fee": 0,
  "id": "7287aab0-29f9-452a-ad1f-5e101c0c76a7",
  "outside_operating_hours": true,
  "status": "CREATED",
  "summary": {
    "number_of_failed_salaries": 7,
    "number_of_finished_salaries": 0,
    "number_of_refunded_salaries": 0,
    "number_of_salaries": 8,
    "number_of_scheduled_salaries": 0
  }
}
