---
title: "Transferir para Contas Stone"
slug: "transferir-para-contas-stone"
draft:false
weight: 3
description > "Faz transferências monetárias para outra conta dentro da Stone. A transferência pode ser agendada, através do campo `scheduled_to`. A data usada no campo `scheduled_to` deve estar entre a data `next_available_execution_date` e a data limite retornada no campo `execution_limit_date` da [API de caléndario de agendamento](https://docs.openbank.stone.com.br/reference#calend%C3%A1rio-de-agendamento) chamada com o parâmetro `operation_type=internal_transfer`. Caso a data escolhida seja menor do que `next_available_execution_date`, a transferência será executada imediatamente. Caso a data seja maior que `execution_limit_date`, será retornado um erro 422. A criação e o agendamento de transferências internas pode acontecer em qualquer dia (incluindo fins de semana e feriados) e em qualquer horário."
---
As transferências internas estão disponíveis 24hs por dia. Elas se referem a transações entre contas Stone.
[block:callout]
{
  "type": "warning",
  "title": "Ciclo de vida assíncrono",
  "body": "As transações são executadas de forma assíncrona, então receber o retorno com código 202 não significa que a transação foi executada. É possível enviar uma transação, receber 202 como retorno e logo depois ocorrer uma falha como, por exemplo, saldo insuficiente.\nTambém é importante lembrar que a transferência precisa de uma aprovação."
}
[/block]