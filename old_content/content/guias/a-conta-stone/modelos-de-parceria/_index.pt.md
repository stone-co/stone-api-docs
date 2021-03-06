---
title: "Modelos De Parceria"
date: 2020-05-14T10:16:28-03:00
lastmod: 2020-05-14T10:16:28-03:00
weight: "2"
draft: false
---
###### Como funcionam os principais modelos de parceria que oferecemos para aqueles que desejam integrar com a nossa API.

------

A Stone oferece dois modelos principais de parceria:

#### Open Banking

Permite que o parceiro integre na [API](https://docs.openbank.stone.com.br/v1.0/reference) para disponibilizar todas as funcionalidades da Conta Stone para a usuária por meio de sua Aplicação. Dessa forma, é possível oferecer à usuária um serviço mais completo, agregando valor ao seu produto.

A usuária interage com seu serviço através de uma interface de sua responsabilidade.

A usuária enxerga a Stone como provedor financeiro, agregando a imagem de confiança financeira da Stone ao seu serviço.

A aprovação de cash-out (qualquer saída de recurso da conta) sempre terá que ser aprovada pela usuária por meio de autenticação no ambiente Stone, através do aplicativo [Aprovador](https://docs.openbank.stone.com.br/docs/aprovacao-guides). Dessa forma, o parceiro fica protegido da responsabilidade na movimentação de recursos financeiros.

#### Conta de Liquidação

Facilita a gestão de operações financeiras complexas, através de um token para operar a sua própria conta com acesso ao Sistema de Pagamentos Brasileiro (SPB). Facilitadores (subadquirentes) e emissores de moeda eletrônica (wallets) podem se beneficiar de uma [API RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) conectada no backbone do Banco Central e integrada no last mile de todos os produtos básicos de conta que você precisa para cash-in e cash-out no seu serviço financeiro. A API de Openbank da Stone foi criada para aguentar um grande número de transações de forma rápida, simples e segura.

Nesse modelo você é a cliente final dona da conta. Não criamos, gerimos ou nos responsabilizamos pelas credenciais de seus clientes em seu ambiente. Todo fluxo financeiro é feito através de sua própria Conta Stone. Todo monitoramento e report de atividade para os reguladores serão feitos levando em consideração o parceiro como cliente final. Por isso, é importante que o parceiro mantenha monitoramento e controles dos seus clientes em seu lado.

Todos os serviços disponíveis na Conta Stone poderão ser oferecidos para seus clientes, com a diferença que o fluxo financeiro é centralizado na sua conta.                      
