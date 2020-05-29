---
title: "Melhorias"
date: 2020-05-14T10:17:00-03:00
lastmod: 2020-05-14T10:17:00-03:00
weight: "2"
draft: false
---

Melhorias tem como função principal a correção de comportamentos não ideais da API. São assim implementas na versão atual da API. As melhorias nunca quebram o fluxo transacional existem, mas podem implicar em mudanças menores em algums trativas. 

Vejas abaixo a lista de melhorias implementadas ou previstas.


_________________



#### Validação de saldo na criação de TEDs, TEFs e Pagamentos

**A quem se aplica:** Aplicações no formato OpenBank. Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado. 

**Sandbox:** Subiu em 28/05/2020

**Produção:** Subida prevista 29/06/2020

**Mudança:** Vamos retirar a validação de saldo na criação de operações nas rotas *`/external_transfer`*, *`/internal_transfer`* e *`/payments`*. Assim o erro *`422: not_enough_funds`* deixará de existir para aplicações que tiverem escopo apenas de criação (modelo openbank).

**Motivação:** Hoje a validação de saldo na criação inviabiliza alguns modelos de negócio em que ter saldo disponível naquele momento não é relevante.

Se você entende que no seu caso de uso o tempo entre a criação e aprovação da usuária é bem curto e que a visualização do saldo é relevante sugerimos que passe a consultar essa informação na rota /balance e apresente a mesma para a usuária na sua interface.  



_________________



#### Agendamento automático de TED criada fora do horário

**A quem se aplica:** Aplicações no formato OpenBank. Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado.

**Sandbox:** Subiu em 28/05/2020

**Produção:** Subida prevista 29/06/2020

**Mudança:** Vamos retirar o agendamento automático na criação de operações na rota *`/external_transfer`*.  Assim continuaremos acatando TEDs fora da janela, mas o campo *`schedule to effective`* virá vazio. 

**Motivação:** Hoje o agendamento automático de TED na criação fora do horário faz com que por vezes a data de execução chegue antes da aprovação por parte da usuária, fazendo com que a transação expire e preciser ser refeita do zero. 

**O que fazer:** Se você tem algum fluxo que depende desse comportamento deverá alterá-lo. Lembrando que o agendamento continuará acontecendo normalmente, só o agendamento automático terá o comportamento alterado. 



_________________



#### Tamanho da chave de idempotência

**A quem se aplica:** Todas as aplicações.

**Sandbox:** Subida prevista em breve

**Produção:** Subida prevista em breve

**Mudança:** Inclusão de limite de *72 caracteres* para a chave de idempotência. 

**O que fazer:** Certifique-se de que sua lógica de idempotência respeita o limite de 72 caracteres. 
