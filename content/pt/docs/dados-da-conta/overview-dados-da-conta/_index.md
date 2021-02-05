---
title: "O Que é Uma Conta"
slug: "overview-dados-da-conta"
hidden: false
createdAt: "2018-12-05T22:14:31.809Z"
updatedAt: "2020-05-01T00:15:00.883Z"
---
[block:api-header]
{
  "title": "Descrição do modelo de contas"
}
[/block]
Em nossa modelagem da conta de pagamentos, temos o conceito de o *user_id* e o *account_id*. Esses conceitos podem ser definidos da seguinte maneira:

* `user_id`: se refere ao identificador do perfil da usuária, contendo informações de dados cadastrais, como por exemplo, nome, apelido e CPF.
* `account_id`: se refere ao identificador da conta da usuária, contendo dados da conta de pagamento.

Essa modelagem foi feita considerando que, antes de uma `user_id` se tornar um `account_id`, ela passa por um processo de *due diligence*, que analisa informações de risco dessa usuária antes dela ter uma conta de pagamentos Stone.
[block:callout]
{
  "type": "info",
  "body": "Todo o processo de Due Diligience da usuária fica sob responsabilidade da Stone e, se aprovada, será gerado um `account_id` para a usuária."
}
[/block]