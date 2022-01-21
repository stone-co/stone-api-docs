---
title: "PADRÕES DA API"
linkTitle: "PADRÕES DA API"
date: 2021-07-12T11:08:00-03:00
lastmod: 2021-07-12T11:08:00-03:00
weight: 1
description: >
      Como utilizar a nossa API
---
<br>
<br>

**Sejam bem-vindos à seção de Referências da API de Banking da Stone.**

Através da nossa API é possível ter funcionalidades de internet banking e de apps de banco no seu negócio!

<br>

## O que é a Stone API Banking
---

<br>

Aqui na Stone a gente acredita não apenas que o **cliente** tem razão, mas que ele **é a nossa razão**. Somos fiéis defensores da competição e acreditamos que isso melhora o mercado como um todo, o que, por sua vez, melhora a vida da nossa razão.

**Foi com base nesse sentimento pró-competição que montamos a Stone Banking API: a primeira API de Banking plugada diretamente no STR.**
A [Conta Stone]({{< relref "/docs/guias/conta-de-pagamento/" >}}) é a nossa oferta para clientes PJ e PF, tanto para aqueles que já pertencem a base da Stone Adquirente, como para aqueles que utilizam outras adquirentes e buscam uma nova forma de se relacionar com sua conta.
  
O Aplicativo da Conta Stone é mais um parceiro da Stone API Banking, usando exatamente os mesmos acessos e APIs descritos nesse documento. \"Eat your own dogfood\" aplicado na prática.

Assim como nós pudemos criar o nosso aplicativo de conta em cima dessa API, você pode fazer o mesmo ou integrar as funcionalidades de automação bancária no seu negócio.

<br>

## O que oferecemos?
---
<br>

Com a API da Conta Stone você pode disponibilizar para os seus clientes:

* Consulta de saldos e extratos;
* Emissão de comprovantes;
* Simulações de transferências e pagamentos antes da efetivação dos mesmos;
* Envio, recebimento e agendamento de transferências tanto de outras Contas Stone como de outros bancos via TED;
* Pagamento, emissão e cancelamento de boletos;
* Pagamento de concessionárias e tributos;
* Cadastro de contatos favorecidos para envio de transferências para outros bancos;
* Link de Pagamento;
* Recargas;
* Pix (Em Alpha).

<br>

## Como funciona a integração?
---
<br>

Por enquanto, ainda não estamos realizando on-board de parceiros em auto-serviço. Por isso, todos os interessados em firmar parcerias devem entrar em contato com o nosso time de parcerias seguindo os seguintes passos:

1. Preencha nosso <a href="https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o" target="_blank"> formulário </a> para receber as informações necessárias para utilizar nossa API em Sandbox.

A partir do preenchimento do formulário vamos registrar a sua Aplicação no nosso sistema e enviar as credenciais de acesso para o [ambiente de Sandbox]({{< relref "/docs/guias/stone-open-banking/#testes-em-sandbox">}}). Além disso, vamos também criar contas de pagamento em Sandbox para você e sua equipe poderem testar a integração.

2. Teste nossas APIS em Sandbox à vontade e, quando estiver pronto, informe ao time de parcerias da Stone através do e-mail parcerias@openbank.stone.com.br.

O processo envolve algumas reuniões presenciais ou por vídeo para a gente entender o melhor qual a melhor forma de integração para o seu negócio.

3. Após tudo integrado, vem a [homologação]({{< relref "/docs/guias/stone-open-banking/#homologação">}}).

A Stone, com a ajuda do parceiro, vai realizar testes na Aplicação ainda em Sandbox para garantir que tudo funciona conforme o esperado e que nenhum cliente vai ser prejudicado por bugs em Produção.

Todo o processo para realização do cadastro se encontra descrito detalhadamente [aqui]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação">}}).

<br>

## Como integrar com a API
---
<br>

Todos os processos e requerimentos para a utilização de nossa API se encontram descritros detalhadamente em nossa [Documentação]({{< relref "/docs/">}}):


#### [Quickstart]({{< relref "/docs/guias/stone-open-banking/#quickstart">}})

Entenda todo o processo de integração com a nossa API.
#### [A Conta Stone]({{< relref "/docs/guias/conta-de-pagamento/">}})

Como funciona este novo produto da Stone, criado para devolver à cliente o controle de sua conta de pagamentos.
#### [Gerar Chaves de Acesso]({{< relref "/docs/guias/token-de-acesso/#gerar-chaves-de-acesso">}})

Passo a passo para obter o par de chaves e receber sua autenticação
#### [Cadastro da aplicação]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação">}})

Como fazer para criar uma aplicação para chamar de sua aqui na Stone.
#### [Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação">}})

Aqui você encontra todos os detalhes sobre o processo de se autenticar na nossa API.
#### [Consentimento]({{< relref "/docs/guias/consentimento/">}})

Descrição de todo o processo de como obter acesso às contas de pagamento de seus clientes.
#### [Webhooks]({{< relref "/docs/guias/webhooks/">}})

Como notificamos o sistema parceiro da ocorrência de eventos.

<br>

---

Para continuar a verificar os padrões da nossa API, siga os links abaixo:
