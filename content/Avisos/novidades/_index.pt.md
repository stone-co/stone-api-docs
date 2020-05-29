---
title: "Melhorias"
date: 2020-05-14T10:17:00-03:00
lastmod: 2020-05-14T10:17:00-03:00
weight: "2"
draft: false
---


#### Link de pagamento 

**A quem se aplica:** Aplicações no formato OpenBank. Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado. 

**Sandbox:** Subiu em 28/05/2020

**Produção:** Subida prevista 29/06/2020

**Mudança:** Vamos retirar a validação de saldo na criação de operações nas rotas *`/external_transfer`*, *`/internal_transfer`* e *`/payments`*. Assim o erro *`422: not_enough_funds`* deixará de existir para aplicações que tiverem escopo apenas de criação (modelo openbank).

**Motivação:** Hoje a validação de saldo na criação inviabiliza alguns modelos de negócio em que ter saldo disponível naquele momento não é relevante.

Se você entende que no seu caso de uso o tempo entre a criação e aprovação da usuária é bem curto e que a visualização do saldo é relevante sugerimos que passe a consultar essa informação na rota /balance e apresente a mesma para a usuária na sua interface.  



_________________



#### Juros, Multas e Descontos na emissão de boletos *cobrança*

**Sandbox:** Subida em prevista em breve

**Produção:** Subida em prevista em breve

**Novidade:** Passaremos a disponibilizar as funcionalidades de Juros, Multas e Descontos na emissão de boletos de cobrança. Os mesmos poderão ser setados com um valor absoluto ou % e a regra poderá se aplicar dado dias corridos ou dias úteis. Essas regras serão configuráveis boleto a boleto. 



_________________



#### URL com HTLM do boleto emitido 

**Sandbox:** Subida em prevista em breve

**Produção:** Subida em prevista em breve

**Novidade:** Passaremos a disponibilizar no response de emissão de boleto uma URL com o boleto já formatado em HTML. 
