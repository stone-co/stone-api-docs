---
title: "Overview"
linkTitle: "Overview"
date: 2020-05-07T18:06:16-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 1
draft: false
description: >

---

**Sejam bem-vindos à seção de Referências da Stone OpenBank API.**

Através da nossa API é possível ter funcionalidades de internet banking e de apps de banco no seu negócio!

#### O que é a Stone OpenBank API

Aqui na Stone a gente acredita não apenas que o **cliente** tem razão, mas que ele **é a nossa razão**. Somos fiéis defensores da competição e acreditamos que isso melhora o mercado como um todo, o que, por sua vez, melhora a vida da nossa razão.

**Foi com base nesse sentimento pró-competição que montamos a Stone OpenBank API: a primeira API de Open Banking plugada diretamente no STR.**
A [Conta Stone](/docs/guias/a-conta-stone/) é a nossa oferta para clientes PJ e PF, tanto para aqueles que já pertencem a base da Stone Adquirente, como para aqueles que utilizam outras adquirentes e buscam uma nova forma de se relacionar com sua conta.
  
O Aplicativo da Conta Stone é mais um parceiro da Stone OpenBank API, usando exatamente os mesmos acessos e APIs descritos nesse documento. \"Eat your own dogfood\" aplicado na prática.

Assim como nós pudemos criar o nosso aplicativo de conta em cima dessa API, você pode fazer o mesmo ou integrar as funcionalidades de automação bancária no seu negócio.

#### O que oferecemos?

Com a API da Conta Stone você pode disponibilizar para os seus clientes:

* Consulta de saldos e extratos;
* Emissão de comprovantes;
* Envio e recebimento de transferências tanto de outras Contas Stone como de outros bancos via TED;
* Pagamento e emissão de boletos;
* Pagamento de concessionárias e tributos;
* Cadastro de contatos favorecidos para envio de transferências para outros bancos;
* Folha de Pagamento;
* Link de Pagamento (Em breve);
* Pix (Em breve).

#### Como funciona a integração?

Por enquanto, ainda não estamos realizando on-board de parceiros em auto-serviço. Por isso, todos os interessados em firmar parcerias devem entrar em contato com o nosso time de parcerias seguindo os seguintes passos:

1. Preencha nosso [formulário](https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o) para receber as informações necessárias para utilizar nossa API em Sandbox.

A partir do preenchimento do formulário vamos registrar a sua Aplicação no nosso sistema e enviar as credenciais de acesso para o [ambiente de Sandbox](/docs/guias/stone-openbank-api/ambientes-da-api/). Além disso, vamos também criar contas de pagamento em Sandbox para você e sua equipe poderem testar a integração.

2. Teste nossas APIS em Sandbox à vontade e, quando estiver pronto, informe ao time de parcerias da Stone através do e-mail parcerias@openbank.stone.com.br.

O processo envolve algumas reuniões presenciais ou por vídeo para a gente entender o melhor [modelo de parceria](/docs/guias/a-conta-stone/modelos-de-parceria/) para o seu negócio.

3. Após tudo integrado, vem a [homologação](/docs/guias/integracao/testando-a-api/).

A Stone, com a ajuda do parceiro, vai realizar testes na Aplicação ainda em Sandbox para garantir que tudo funciona conforme o esperado e que nenhum cliente vai ser prejudicado por bugs em Produção.

Todo o processo para realização do cadastro se encontra descrito detalhadamente [aqui](/docs/guias/integracao/cadastro-da-aplicacao/).

#### Como integrar com a API

Todos os processos e requerimentos para a utilização de nossa API se encontram descritros detalhadamente em nossa [Documentação](/docs/):

#### [Quickstart](/docs/guias/stone-openbank-api/quickstart/)

Faça a sua primeira movimentação financeira de teste seguindo esses três passos!

#### [Ambientes da API](/docs/guias/stone-openbank-api/ambientes-da-api/)

Como funcionam nossos ambientes de Sandbox e Produção.

#### [A Conta Stone](/docs/guias/a-conta-stone/)

Como funciona este novo produto da Stone, criado para devolver à cliente o controle de sua conta de pagamentos.

#### [Modelos de Parceria](/docs/guias/a-conta-stone/modelos-de-parceria/)

Como funcionam os principais modelos de parceria que oferecemos para aplicações que desejam integrar com a nossa API.

#### [Aplicativos](/docs/guias/a-conta-stone/aplicativos/)

O que são os aplicativos desenvolvidos pela Stone e por parceiros.

#### [Cadastro da Aplicação](/docs/guias/integracao/cadastro-da-aplicacao/)

Passo a passo para obter acesso e conseguir se autenticar em nossa API de [Sandbox](/docs/guias/stone-openbank-api/ambientes-da-api/#ambiente-de-sandbox).

#### [Autenticação](/docs/guias/integracao/autenticacao/)

Aqui você encontra todos os detalhes sobre o processo de se autenticar na nossa API.

#### [Testando a API](/docs/guias/integracao/testando-a-api/)

Teste nossa API no ambiente de [Sandbox ](/docs/guias/stone-openbank-api/ambientes-da-api/#ambiente-de-sandbox) para garantir que tudo funciona conforme o esperado e que nenhuma cliente vai ser prejudicada por bugs em Produção.

#### [Consentimento](/docs/guias/integracao/consentimento/)

Descrição de todo o processo de como obter acesso às contas de pagamento de suas clientes.

#### [Aprovação](/docs/guias/integracao/aprovacao/)

Como o dono da conta permite que uma transação criada pelo parceiro seja realizada.

#### [Webhooks](/docs/guias/integracao/webhooks/)

Como notificamos o sistema parceiro da ocorrência de eventos.

#### [Boas Práticas](/docs/guias/integracao/boas-praticas/)

Como armazenar dados e realizar operações em nossa API de forma segura.
