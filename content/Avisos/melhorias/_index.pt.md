---
title: "Melhorias"
date: 2020-05-14T10:17:00-03:00
lastmod: 2020-05-14T10:17:00-03:00
weight: "2"
draft: false
---

Melhorias tem como função principal a correção de comportamentos não ideais da API. São assim implementas na versão atual da API. As melhorias nunca quebram o fluxo transacional existem, mas podem implicar em mudanças menores em algums trativas. 

Vejas abaixo a lista de melhorias implementadas e previstas.
<br>
<br>
# Melhorias Previstas
<br>
<br>
<br>
#### Agendamento automático de TED criada fora do horário
_________________
**A quem se aplica:** Aplicações no formato OpenBank. Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado.

**Sandbox:** Subiu em ?

**Produção:** Subida prevista ?

**Mudança:** Vamos retirar o agendamento automático na criação de operações na rota *`/external_transfer`*.  Assim continuaremos acatando TEDs fora da janela, mas o campo *`schedule to effective`* virá vazio. 

**Motivação:** Hoje o agendamento automático de TED na criação fora do horário faz com que por vezes a data de execução chegue antes da aprovação por parte da usuária, fazendo com que a transação expire e preciser ser refeita do zero. 

**O que fazer:** Se você tem algum fluxo que depende desse comportamento deverá alterá-lo. Lembrando que o agendamento continuará acontecendo normalmente, só o agendamento automático terá o comportamento alterado. 
<br>
<br>
<br>

# Melhorias Implementadas
<br>
<br>
<br>
#### Mudança do nome do objeto payer
_________________

**A quem se aplica:** Todas as aplicações que fazem emissão de boleto. 

**Sandbox:** Subiu em ?

**Produção:** Subiu em ?

**Mudança:** O objeto `payer` passou a se chamar `customer`.

**Motivação:** Para evitar confusões entre pagador que consta no registro do boleto e o pagador de fato do boleto fizemos algumas mudanças de nomeclatura. O objeto `payer` enviado na criação do boleto passará a se chamar `customer` e `payer` passará a ser sempre referente a quem de fato efetuou o pagamento. 

**O que fazer:** A API continuará aceitando a criação de boleto com objeto `payer`para que não haja quebra dos parceiros já integrados. Assim, não há uma mudança obrigatória na forma como você já implementou, mas sugerimos fortemente que assim que possível você migre para a nova estrutura. 
<br>
<br>
<br>

#### Notificação por e-mail e push para parceiros no formato Conta de Liquidação
_________________

**A quem se aplica:** Aplicações no formato Conta de Liquidação. Essa mudança é válida apenas quando a aprovação da transação é feita via API pela própria aplicação. 

**Sandbox:** Subiu em 

**Produção:** Subiu em 

**Mudança:** Paramos de enviar e-mails e pushs de notificação referentes a cahs-outs para usuários quando a transação foi aprovada diretamente pela API. Quando as transações são de cash-in os usuários continuando sendo notificados normalmente. 

**Motivação:** Parcerios do modelo Conta de Liquidação costumam ter um número muito grande de movimentaçãoes e fazendo com que o número de notificações seja muito alto e acab perdem seu propósito. 
<br>
<br>
<br>
#### Validação de saldo na criação de TEDs e TEfs
_________________

**A quem se aplica:** Aplicações no formato OpenBank. Essa mudança é válida apenas quando a criação e a provação são feitas em momentos diferentes. Aplicações que tem escopo de criação e aprovação não terão o comportamento afetado. 

**Sandbox:** Subiu em 28/05/2020

**Produção:** Subiu em 22/07/2020

**Mudança:** Vamos retirar a validação de saldo na criação de operações nas rotas *`/external_transfer`*, *`/internal_transfer`* e *`/payments`*. Assim o erro *`422: not_enough_funds`* deixará de existir para aplicações que tiverem escopo apenas de criação (modelo openbank).

**Motivação:** Hoje a validação de saldo na criação inviabiliza alguns modelos de negócio em que ter saldo disponível naquele momento não é relevante.

**O que fazer:** Se você entende que no seu caso de uso o tempo entre a criação e aprovação da usuária é bem curto e que a visualização do saldo é relevante sugerimos que passe a consultar essa informação na rota /balance e apresente a mesma para a usuária na sua interface.  
<br>
<br>
<br>
#### Tamanho da chave de idempotência
_________________

**A quem se aplica:** Todas as aplicações.

**Sandbox:** Subiu em 03/05/2020

**Produção:** Subiu em 03/05/2020

**Mudança:** Incluimos um limite máximo de 72 caracteres para as chaves de idempotência. Chamadas feitas com uma chave com tamanho superior a 72 caracteres retornará um erro HTTP 431.

**O que fazer:** Fizemos uma análise e nenhum parceiro em produção utiliza chaves acima do limite setado. Pedimos que se certifique que sua lógica de idempotência não é crescente de forma a alcançar esse limite em algum momento e que caso seja faça as devidas alterações.
<br>
<br>
<br>
