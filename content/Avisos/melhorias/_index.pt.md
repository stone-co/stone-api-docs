---
title: "Melhorias"
date: 2020-05-14T10:17:00-03:00
lastmod: 2020-05-14T10:17:00-03:00
weight: "2"
draft: false
---


### Validação de saldo na criação de TEDs, TEFs e Pagamentos

Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado. 

**Sandbox:** Subiu em 28/05/2020

**Produção:** Subida prevista 29/06/2020

**Motivação:** Hoje a validação de saldo na criação inviabiliza alguns modelos de negócio em que ter saldo disponível naquele momento não é relevante.

**Mudança:** Vamos retirar a validação de saldo na criação de operações de *`/external_transfer`*, *`/internal_transfer`* e *`/payments`*. Assim o erro *`422: not_enough_funds`* deixará de existir para aplicações que tiverem escopo apenas de criação (modelo openbank).

Se você entende que no seu caso de uso o tempo entre a criação e aprovação da usuária é bem curto e que a visualização do saldo é relevante sugerimos que passe a consultar essa informação na rota /balance e apresente a mesma para a usuária na sua interface.  



_________________



### Agendamento automático de TED criada fora do horário

Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado.

**Sandbox:** Subiu em 28/05/2020

**Produção:** Subida prevista 29/06/2020

**Motivação:** Hoje o agendamento automático de TED na criação fora do horário faz com que por vezes a data de execução chegue antes da aprovação por parte da usuária, fazendo com que a transação expire e preciser ser refeita do zero. 

**Mudança:** Vamos retirar o agendamento automático na criação fora do horáio de TEDs (*/external_transfer*).  Assim continuaremos acatando TEDs fora da janela, mas o campo *`schedule to effective`* virá vazio. 

Se você costuma mostrar pra sua usuária da data de agendamento logo após uma TED criada fora do horário esse comportamento dexará de existir. 
