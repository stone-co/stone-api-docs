---
title: "Overview"
slug: "Overview"
hidden: false
weight: 1
date: "2019-11-19T14:32:50.860Z"
lastmod: "2019-11-19T22:48:16.424Z"
---


<br>

Sejam bem-vindos à documentação da Conta Stone SDK. Através da Conta Stone SDK é possível fazer o processo de abertura de conta e login no Stone OpenBank.



---


#### **Introdução**


A Conta Stone SDK é o ponto de entrada para acesso às nossas SDKs de autenticação (Auth SDK), aprovação (Approver SDK) e verificação de [KYC](https://en.wikipedia.org/wiki/Know_your_customer) (_Know your costumer_) (Pegasus SDK). 

Segue abaixo um diagrama de como funciona a comunicação entre esses três atores.


![imagem_conta_stone_sdk_diagram](/docs/guias/conta-stone-sdk/overview/conta-stone-sdk-diagram.png)


- Auth SDK - responsável por executar todo o processo de autenticação seguindo as diretrizes do [oAuth2](https://oauth.net/2/).

- Approver SDK - realiza todo o processo de aprovação e rejeição de transações.

- Pegasus SDK - SDK de KYC, responsável por capturar as informações do usuário que está realizando cadastro na conta.


<br>


#### **Como integrar com a SDK**


Antes de começar a integração é necessário obter uma chave de acesso ao nosso repositório. Para obter esta chave, entre em contato com a gente [aqui](https://app.pipefy.com/public/form/Qz4ptt_W?origem_do_lead=%22Documenta%C3%A7%C3%A3o%22). 

Para integrar com o **iOS**, acesse [aqui](/docs/guias/conta-stone-sdk/sdk-sample-ios).

Para integrar com o **Android**, acesse [aqui](/docs/guias/conta-stone-sdk/sdk-sample-android).