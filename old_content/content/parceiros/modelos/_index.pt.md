---
title: "Modelos de Parceria"
date: 2020-05-14T14:48:15-03:00
lastmod: 2020-05-14T14:48:15-03:00
weight: "1"
draft: false
---

Existem dois modelos principais de parcerias. No primeiro você cria uma aplicação para gerenciar sua própria Conta Stone pela API, esse modelo é chamado de **Conta de Liquidação**. Já no modelo de **OpenBank** a integração é construída para automatizar o funcionalmento de algum serviço com a Conta Stone e essa integração será disponibilizada para todos que utilizam esse serviço "plugarem" suas Contas Stone e aproveitarem as vantegsn de processo mais fluídos. 

Veja abaixo em mais detalhes o que cada modelo trás de possibilidades.



_________________



### OpenBank

No modelo de OpenBank você pode integrar seu sistema a nossa API e disponibilizar todas as funcionalidades da Conta Stone para a usuária por meio de sua Aplicação. Esse modelo é ideal para ERPs, sistemas contábeis e sistemas de gestão que querem oferecer para seus clientes uma experiência fluída e sem retrabalho.
	
Ao integrar a API será possível que a usuária consulte a informações da sua Conta Stone e inicie transações diretamente da sua interface reduzindo drasticamente o retrabalho e mitigando erros no processo. 
	
Manter o controle na mão da usuária é imprescindível. Por isso, depois de criar sua Conta Stone, a usuária terá que dar [consentimento](https://docs.openbank.stone.com.br/docs/consentimento-guides) para que sua aplicação possa operar a conta. O processo de consentimento é feito uma única vez. 
Além disso, todas as movimentações que envolverem retirara de dinheiro da conta (*cash out*) deverão ser aprovadas ou reprovadas pela usuária pelo nosso App Aprovador ou App da Conta Stone. Para facilitar o processo permitimos aprovações individuais ou em lote pela usuária. 
	
Nesse modelo é possível oferecer para a sua usuária as seguintes operações:
  * Iniciação de transferências para outras contas Stone;
  * Iniciação TEDs para contas de outros bancos;
  * Iniciação agendamentos de TEDs e transferências;
  * Iniciação pagamento de boletos;
  * Iniciação pagamento de tributos e concessionárias com código de barras;
  * Iniciação agendamento de pagamentos;
  * Emissão boletos de cobrança;
  * Emissão boletos de proposta;
  * Emissão boletos de depósito;
  * Emissão comprovantes;
  * Consulta de extrato;
  * Gerenciamento contatos.  
  
_________________

### Conta de Liquidação

No modelo de conta liquidação você pode movimentar sua Conta Stone por meio de uma API RESTful com as todas as funcionalidades para cash-in e cash-out.
	
Esse modelo é especialmente vantajoso para empresas que tem operações financeiras complexas com o desafio de gerenciar um grande número de movimentações em sua conta, como é o caso de Facilitadores (subadquirentes) e Emissores de moeda eletrônica (wallets).
	
É possível automatizar processos e rotinas do seu time financeiro poupando tempo, reduzindo custos e mitigando erros. Você pode integrar o seu sistema de gestão interno à sua Conta acabando com o rebatrabalho de fazer lançamentos em dois sistemas, criação e inserção de arquivos no sistema dos bancos.
	
Nesse modelo você poderá operar sua própria Conta Stone e realizar todo o fluxo financeiro por meio de um token com acesso direto ao Sistema de Pagamentos Brasileiros. Nós não criamos, gerimos ou nos responsabilizamos pelas credenciais de seus clientes em seu ambiente. Por isso é importante que você mantenha o monitoramento e controle dos seus clientes. Todos os relatórios de atividades para os reguladores serão feitos considerando a sua conta como cliente final.

Com essa solução é possível gerenciar sua conta 100% via API, operando:
  * Transferências para outras contas Stone;
  * TEDs para contas de outros bancos;
  * Agendamentos de TEDs e transferências;
  * Pagamentos de boletos;
  * Pagamentos de tributos e concessionárias com código de barras;
  * Agendamentos de pagamentos;
  * Emissão de boletos de cobrança;
  * Emissão de boletos de proposta;
  * Emissão de boletos de depósito;
  * Emissão de comprovantes;
  * Consulta de extrato;
  * Folha de pagamento;
  * Gerenciamento de contatos.
  
_________________


#### Se interessou? Entre em contato com nosso time comercial por *[aqui](https://app.pipefy.com/public/form/Qz4ptt_W?origem_do_lead="Formulário%20comercial%20documentação")*.
