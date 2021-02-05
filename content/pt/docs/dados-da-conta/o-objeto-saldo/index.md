---
title: "O Objeto Saldo"
slug: "o-objeto-saldo"
hidden: false
createdAt: "2020-03-10T17:31:02.853Z"
updatedAt: "2020-03-11T00:25:58.393Z"
---
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "balance",
    "1-0": "blocked_balance",
    "2-0": "scheduled_balance",
    "2-1": "Soma do valor de transações agendadas. Não tem relação direta com o saldo da conta, podendo inclusive ter um valor maior que o mesmo.",
    "0-1": "Saldo da conta livre para movimentação. Deve ser somado ao `blocked_balance` para calcular o saldo total.",
    "1-1": "Saldo da conta bloqueado. Deve ser somado ao `balance` para calcular o saldo total.",
    "0-2": "*Integer*",
    "1-2": "*Integer*",
    "2-2": "*Integer*"
  },
  "cols": 3,
  "rows": 3
}
[/block]