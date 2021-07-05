---
title: "Cadastro da Aplicação"
linkTitle: "Cadastro da Aplicação"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 3
draft: true
description: >

---

Qualquer parceiro ou cliente que deseje acessar e/ou movimentar a sua conta ou de terceiros pela nossa API precisará ter sua aplicação identificada. O identificador que representa a sua aplicação na Stone é chamado ClientID. 

O ClientID será usado no processo de Autenticação, permitindo a identificação da origem dos requests feitos por API. Ou seja, ele será usado no seu Token de Acesso para realizar chamadas. O ClientID é gerado pela Stone, é único e não será alterado posteriormente. 

Para obter um ClientID, você deverá entrar em [contato](https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o) com nosso time comercial. Em seguida, pediremos algumas informações para cadastrar sua aplicação. Neste formulário, será necessário enviar ao time da Stone:

1. A sua [chave pública](/docs/guias/token-de-acesso/gerar-chaves-de-acesso/) - que será atrelada ao cadastro da sua aplicação
2. Uma URI de Redirect - precisamos de um local público para redirecionarmos o usuário final depois que ele aprovar ou reprovar o [Consentimento](/docs/guias/consentimento/overview/) de acesso à sua plataforma. Caso você esteja fazendo a integração para acesso à sua própria conta, pode desconsiderar essa etapa. 
3. Uma URI de Webhooks - Precisamos de um local público para enviar mudanças de estado das contas para aplicações. Essa URI irá receber as informações das Webhooks para seu processamento.
4. Sua Linguagem de desenvolvimento - Nossa infraestrutura disponibiliza uma API RESTful com respostas em JSON.

Após o recebimento de todas as informações e cadastro da sua aplicação, enviaremos o seu ClientID por e-mail. 

Atenção! O ClientID será enviado para o e-mail identificado no formulário como dono da aplicação. Caso você queira movimentar a sua própria conta, este e-mail deverá ser o mesmo cadastrado no momento de [abertura da Conta](/docs/guias/conta-de-pagamento/abertura-de-conta/).

Pronto! Com seu ClientID em mãos, você já pode realizar o processo de [Autenticação](/docs/guias/token-de-acesso/autenticacao/). 
