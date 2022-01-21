---
title: "STONE API BANKING"
linkTitle: "STONE API BANKING"
date: 2021-08-05T15:40:00-03:00
lastmod: 2021-08-05T15:40:00-03:00
weight: 1
draft: false

description: >
    
---
<br>

## Overview
---

<br>

**Seja bem-vindo à documentação da API de Banking da Stone!**
<br>

Segundo o Banco Central, o Open Banking / Open Finance, ou sistema financeiro aberto, é a possibilidade de clientes de produtos e serviços financeiros permitirem o compartilhamento de suas informações entre diferentes instituições autorizadas pelo Banco Central e a movimentação de suas contas bancárias a partir de diferentes plataformas e não apenas pelo aplicativo ou site do banco, de forma segura, ágil e conveniente.

Como na Stone somos fiéis defensores da competição e temos o cliente como nossa razão de existir, acreditamos na revolução proporcionada por esse sistema e construímos a primeira API de Banking plugada diretamente no coração do STR. Acreditamos que nosso produto poderá gerar novos modelos de negócios, dar maior controle e transparência, além de permitir automatizações e ganho de eficiência para as empresas. 

A partir da integração e do uso da API Stone Banking, você poderá movimentar a sua própria conta Stone por meio de uma API RESTful com todas as funcionalidades de cash-in e cash-out. Caso você tenha uma plataforma, também poderá solicitar acesso a contas terceiras para disponibilizar funcionalidades financeiras e agregar ainda mais valor ao seu produto. É claro que para acessar e iniciar transações em contas terceiras, será preciso obter o Consentimento do usuário dono da conta, um conceito essencial para o bom funcionamento do Open Banking.

Nesta documentação, você pode explorar todos os produtos e funcionalidades que a nossa API oferece! Além disso, como todas as chamadas em nossa API deverão ser autenticadas para identificação do sujeito de cada ação, vamos detalhar como funciona o acesso via token. 
<br>

Para iniciar, confira um passo a passo da nossa integração abaixo aqui no [Quickstart]({{< relref "/docs/guias/stone-open-banking/#quickstart" >}})! 

<br>

## Quickstart
---


##### Contato Comercial 

Para realizar chamadas em nossa API, primeiro precisamos que você preencha este <a href="https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o" target="_blank">formulário</a>.

Nosso time de parcerias entrará em contato em até 24 horas para entender seu modelo de negócio e te apresentar a proposta mais adequada.

Você também receberá um contrato para formalização da parceria.

Por enquanto, ainda não estamos realizando onboarding de parceiros em autosserviço, mas queremos liberar isso em breve! 
<br>
<br>

##### Testes em Sandbox

Após o contato com nosso time, você receberá o formulário para testes em ambiente de Sandbox, que deverá ser preenchido contendo a sua [Chave Pública]({{< relref "/docs/guias/token-de-acesso/#gerar-chaves-de-acesso" >}}). 
Quando recebermos essa chave, faremos o [Cadastro da sua Aplicação]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação" >}}) e te retornaremos um ClientID, o seu identificador único aqui na Stone. 

Com o ClientID em mãos, você já pode fazer o processo de [Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação" >}}), que terá como resultado a liberação do seu Access Token ou [Token de Acesso]({{< relref "/docs/guias/token-de-acesso/#overview" >}}) e realizar as [chamadas autenticadas]({{< relref "/docs/guias/token-de-acesso/#chamada-autenticada" >}}) em Sandbox. 

<br>

**Pronto!** Agora você já pode começar os testes e realizar ações em nossa API - em ambiente de Sandbox. 
<br>
<br>

##### Homologação

Assim que os testes em Sandbox forem finalizados, vamos te guiar no processo de Homologação. 

Esse processo consiste em executar todas as ações que a sua aplicação tem permissão para fazer, numa sequência definida e com o acompanhamento e registro pela equipe da Stone. 

O objetivo é garantir que tudo esteja funcionando como esperado e que você tenha acesso a todos os recursos necessários.
<br>
<br>

##### Produção

Finalmente, para integrar em ambiente de Produção, você vai nos enviar uma nova Chave Pública - iremos solicitar em um Formulário para Virada em Produção - para que a gente gere o seu ClientID de Produção. Você vai realizar as mesmas etapas que já fez para obtenção do Access Token em Sandbox, que permitirá a realização de [Chamadas Autenticadas]({{< relref "/docs/guias/token-de-acesso/#chamada-autenticada" >}}). 

Caso você tenha uma plataforma, ERP ou outro sistema e deseje realizar ações em uma conta de outro usuário (um cliente seu, por exemplo), você deverá pedir o [Consentimento]({{< relref "/docs/guias/consentimento/">}}) dele para realização das chamadas. Caso seja para sua própria conta, pode desconsiderar esse processo, mas lembre-se de que você precisará [abrir uma Conta Stone]({{< relref "/docs/guias/conta-de-pagamento/#abertura-de-conta" >}}). 

**Atenção!** Ressaltamos que os dois ambientes disponíveis são completamente separados, ou seja, usuários criados em ambiente de Sandbox não existem em Produção e vice-versa. Vale lembrar que os ambientes, em termos de funcionalidades, são exatamente iguais.

**Importante!** O acesso ao ambiente de Produção só será liberado depois que os testes em Sandbox forem realizados e o roteiro de Homologação for validado. 

Confira abaixo as URLs para acesso aos ambientes:

| Ambiente | Endpoint de acesso |
| -------- | ------------------ |
| Sandbox  | https://sandbox-api.openbank.stone.com.br |
| Produção | https://api.openbank.stone.com.br |


<br>

