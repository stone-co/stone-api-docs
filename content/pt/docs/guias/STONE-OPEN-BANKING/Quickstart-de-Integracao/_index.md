---
title: "Quickstart"
linkTitle: "Quickstart"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 2
draft: false

description: >

---

#### Contato Comercial 

Para realizar chamadas em nossa API, primeiro precisamos que você preencha este <a href="https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o" target="_blank"> formulário </a>.

Nosso time de parcerias entrará em contato em até 24 horas para entender seu modelo de negócio e te apresentar a proposta mais adequada.

Você também receberá um contrato para formalização da parceria.

Por enquanto, ainda não estamos realizando onboard de parceiros em autosserviço, mas queremos liberar isso em breve! 
<br>
<br>

#### Testes em Sandbox

Após contato com nosso time, você receberá o formulário para testes em  ambiente de Sandbox, que deverá ser preenchido contendo a sua [Chave Pública](/docs/guias/token-de-acesso/gerar-chaves-de-acesso/). 
Quando recebermos essa chave, faremos o [Cadastro da sua Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/) e te retornaremos um ClientID, o seu identificador único aqui na Stone. 

Com o ClientID em mãos, você já pode fazer o processo de [Autenticação](/docs/guias/token-de-acesso/autenticacao/), que terá como resultado a liberação do seu Access Token, ou seu [Token de Acesso](/docs/guias/token-de-acesso/overview/). 

<br>

**Pronto!** Agora você já pode começar os testes e realizar ações em nossa API - em ambiente de Sandbox. 
<br>
<br>

#### Homologação

Assim que os testes em Sandbox forem finalizados, vamos te guiar no processo de Homologação. 

Esse processo consiste em executar todas as ações que a sua Aplicação tem permissão para fazer, numa sequência definida e com o acompanhamento e registro pela equipe da Stone. 

O objetivo é garantir que tudo esteja funcionando como esperado e que você tenha acesso a todos os recursos necessários.
<br>
<br>

#### Produção

Finalmente, para integrar em Ambiente de Produção você vai nos enviar uma nova Chave Pública - iremos solicitar em um Formulário para Virada em Produção - para que a gente gere o seu ClientID de Produção. Você vai realizar as mesmas etapas que já fez para obtenção do Access Token, que permitirá a realização de [Chamadas Autenticadas](/docs/guias/token-de-acesso/chamada-autenticada/). 

Caso você tenha uma plataforma, ERP ou outro sistema e deseje realizar ações em uma conta de outro usuário (um cliente seu, por exemplo), você deverá pedir o [Consentimento](/docs/guias/consentimento/overview/) do mesmo para realização das chamadas. Caso seja para sua própria conta, pode desconsiderar esse processo, mas lembre-se de que você precisará [abrir uma Conta Stone](/docs/guias/conta-de-pagamento/abertura-de-conta/). 

**Atenção!** Ressaltamos que os dois ambientes disponíveis são completamente separados, ou seja, usuários criados em ambiente de Sandbox não existem em Produção, e vice-versa. Vale lembrar que os ambientes, em termos de funcionalidades, são exatamente iguais.

**Importante!** O acesso ao ambiente de Produção só será  liberado após testes em Sandbox realizados e roteiro de Homologação validado. 

Confira abaixo as URLs para acesso aos ambientes:

| Ambiente | Endpoint de acesso |
| -------- | ------------------ |
| Sandbox  | https://sandbox-api.openbank.stone.com.br |
| Produção | https://api.openbank.stone.com.br |

