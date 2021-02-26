---
title: "original-Consultar Extrato"
slug: "original-consultar-extrato"
hidden: true
draft: true
date: "2018-12-10T14:35:21.601Z"
lastmod: "2019-02-21T20:18:22.067Z"
---
[block:callout]
{
  "type": "warning",
  "title": "Valor da operação",
  "body": "Também repare que, quando se faz uma transferência de R$100,00, por exemplo, o campo _operation_amount_ terá valor de 10000 centavos. Já o campo _amount_ será a soma do valor da operação com a taxa cobrada (_fee_amount_)."
}
[/block]
Note que, na resposta acima, foram feitas duas transferências, uma interna e uma externa, ambas com as suas particularidades de retorno.

Obs: O extrato é dividido por tipos de movimentação. É possível consultar qual foi a movimentação pelo `type` da resposta. No exemplo acima, podemos notar que tivemos duas movimentações: uma transferência interna (`type:internal`) e uma transferência externa (`type:external`), ambas com campos de resposta diferentes.
