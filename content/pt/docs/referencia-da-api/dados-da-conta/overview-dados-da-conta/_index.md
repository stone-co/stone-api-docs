---
title: "O Que é Uma Conta"
slug: "overview-dados-da-conta"
hidden: false
date: 2018-12-05T22:14:31.809Z
lastmod: 2020-05-01T00:15:00.883Z
weight: 2
description: >

---

Descrição do modelo de contas.

---

Em nossa modelagem da conta de pagamentos, temos o conceito de  *user_id* e  *account_id*.
Esses conceitos podem ser definidos da seguinte maneira:

* `user_id`: se refere ao identificador do perfil do usuário, contendo informações de dados cadastrais, como por exemplo, nome, apelido e CPF.

* `account_id`: se refere ao identificador da conta do usuário, contendo dados da conta de pagamento.

Essa modelagem foi feita considerando que, antes de um `user_id` se tornar um `account_id`, ele passa por um processo de *due diligence*, que analisa informações de risco desse usuário antes dele ter uma conta de pagamentos Stone.

{{% pageinfo %}}
**Atenção**

Todo o processo de Due Diligence do usuário fica sob responsabilidade da 
Stone e, se aprovada, será gerado um `account_id` para o usuário.
{{% /pageinfo %}}
