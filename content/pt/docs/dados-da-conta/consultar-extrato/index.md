---
title: "Consultar Extrato"
slug: "consultar-extrato"
hidden: false
createdAt: "2019-04-01T19:05:11.368Z"
updatedAt: "2020-04-20T20:28:41.079Z"
---

{
  "type": "info",
  "title": "Valor da operação",
  "body": "Também repare que, quando se faz uma transferência de R$100,00, por exemplo, o campo _operation_amount_ terá valor de 10000 centavos. Já o campo _amount_ será a soma do valor da operação com a taxa cobrada (_fee_amount_)."
}


[block:callout]
{
  "type": "warning",
  "body": "O extrato é dividido por tipos de movimentação. É possível consultar qual foi a movimentação pelo `type` da resposta. No exemplo acima, podemos notar que tivemos duas movimentações: uma transferência interna (`type:internal`) e uma transferência externa (`type:external`), ambas com campos de resposta diferentes. Veja neste [link](https://docs.openbank.stone.com.br/reference#objetos-do-extrato) para mais informações sobre o JSON Schema de cada tipo de operação.",
  "title": "Tipos diferentes de extratos"
}
[/block]
Note que, na resposta acima, foram feitas duas transferências, uma interna e uma externa, ambas com as suas particularidades de retorno.

Em cada extrato há duas informações: {balance before} e {balance after}. O balance before registra o saldo do usuário antes da operação, e o balance after registra o saldo após a operação dado o balance before menos o valor da operação.