---
title: "O Objeto Saldo"
slug: "o-objeto-saldo"
hidden: false
createdAt: "2020-03-10T17:31:02.853Z"
updatedAt: "2020-03-11T00:25:58.393Z"
weight: 5
---
<br>

| Chave             | Descrição                                                               | Total        |
| ------------------| ------------------------------------------------------------------------|--------------|
| balance           | Saldo da conta livre para movimentação. Deve ser somado ao `blocked_balance` para calcular o saldo total.| *Integer*     |
| blocked_balance   | Saldo da conta bloqueado. Deve ser somado ao `balance` para calcular o saldo total.| *Integer*     |
| scheduled_balance | Soma do valor de transações agendadas. Nâo tem relação direta com o saldo da conta, podendo inclusive ter um valor maior que o mesmo.| *Integer*     |                  
