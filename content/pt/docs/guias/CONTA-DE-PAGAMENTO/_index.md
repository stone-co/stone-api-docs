---
title: "CONTA DE PAGAMENTO"
linkTitle: "CONTA DE PAGAMENTO"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 3
draft: false
description: >

---
<br>

## Overview
---
<br>

Somos uma Instituição de Pagamentos emissora de moeda eletrônica autorizada pelo Banco Central e por isso podemos oferecer uma Conta de Pagamento. 
<br>Nesse tipo de conta, os recursos devem ser depositados previamente, ou seja, oferecemos uma conta do tipo pré-paga aos nossos clientes. Dessa forma, não haverá geração de fatura nem saldo negativo.


Através de uma conta de pagamento, você tem acesso a serviços financeiros sem precisar ir a um banco. É possível fazer e receber Pix, TEDs, como também realizar o pagamento de boletos e outros serviços básicos de uma conta corrente. 
<br>Além disso, toda a gestão da conta pode ser feita online, simplificando atividades do dia a dia. Inclusive, para abrir uma conta, você não precisa se deslocar até uma agência. Mesmo assim, se precisar de alguém para te ajudar, a Stone está disponível para contato.


Caso ainda não possua uma conta para movimentar por meio do seu Token de Acesso, você pode realizar o processo de [Abertura de Conta]({{< relref "/docs/guias/conta-de-pagamento/#abertura-de-conta">}}) pelo nosso App (disponível para [iOS](https://apps.apple.com/br/app/stone/id1438680035) e [Android](https://play.google.com/store/apps/details?id=co.stone.banking.mobile.flagship&hl=pt_BR&gl=US)). Esse processo também deve ser feito caso você seja uma plataforma e deseje oferecer abertura de conta Stone aos seus clientes, pois também precisaremos do seu perfil cadastrado aqui. 


O processo de abertura de conta pode ser resumido em duas etapas que serão detalhadas a seguir:<br>
1. [Envio de Dados Cadastrais]({{< relref "/docs/guias/conta-de-pagamento/#envio-de-dados-cadastrais">}})
2. [Realização do processo de KYC (Know Your Customer)]({{< relref "/docs/guias/conta-de-pagamento/#kyc-know-your-customer">}})

<br>

## Abertura de Conta
---


### **Envio de Dados Cadastrais**

O processo de abertura de conta será iniciado quando o usuário preencher os dados básicos de cadastro para criação de sua identidade na Stone. A identidade é o perfil do usuário na Stone e será gerido sempre por nós. Os dados solicitados nesta etapa serão Nome Completo, CPF, CNPJ, Razão Social e E-mail. 


**Atenção!**
<br>Para contas do tipo Pessoa Jurídica, a abertura deverá ser feita obrigatoriamente por um sócio ou responsável legal. Dependendo do tipo de cadastro, poderemos solicitar ainda alguns documentos como comprovante de MEI, Registro em Junta Comercial, entre outros. 


O recebimento dos dados iniciais pela Stone pode ser feito via aplicativo ([iOS](https://apps.apple.com/br/app/stone/id1438680035) e [Android](https://play.google.com/store/apps/details?id=co.stone.banking.mobile.flagship&hl=pt_BR&gl=US)) com o usuário dono da conta realizando o processo de preenchimento diretamente pelo app ou pode ser feito por API, caso você seja uma plataforma e queira oferecer o [processo de abertura de conta Stone]({{< relref "/docs/referencia-da-api/dados-da-conta/criar-nova-conta-de-pagamento/">}}) em seu produto. 
<br>Caso escolha realizar o processo por API, após o recebimento dos dados cadastrais, faremos uma primeira validação e, em seguida, iremos disparar um e-mail para criação de senha de acesso pelo usuário. 


**Credenciais**: A identidade é acessada através das credenciais do usuário, como, por exemplo, um e-mail e uma senha. Hoje essas credenciais dão acesso apenas ao perfil do usuário na Stone e não estão relacionadas às credenciais usadas por outros serviços que podem estar integrados à Conta Stone, como o Guiabolso, por exemplo. Entretanto, o objetivo é que no futuro a identidade na Stone funcione como uma conta de usuário no Google ou no Facebook, por exemplo. A partir de um único conjunto de credenciais, será possível se conectar a vários serviços.


**Pronto!** Com e-mail validado e senha criada, o usuário já pode realizar o processo de KYC (Know Your Customer).

<br>


### **KYC (Know Your Customer)**

Como somos regulados pelo Banco Central, temos a responsabilidade de realizar uma análise de documentos e procedimentos chamados KYC (Know Your Customer). Essa análise é realizada com cuidado internamente para evitar fraudes, principalmente falsidade ideológica. 


Nesse processo, solicitamos algumas informações além dos dados já enviados pelo cliente, como selfies e fotos de documentos. Todas as informações são analisadas para que o cadastro do usuário seja aprovado ou não. 


Com todas as validações feitas e aprovadas, o usuário terá sua conta aberta e pronta para uso.
Para plataformas que queiram oferecer o processo de abertura de conta Stone de maneira integrada, o envio das informações iniciais poderá ser feito usando nossa API. Já para recebimento dos dados de KYC, será necessário o uso da nossa SDK - detalhada na [seção exclusiva]({{< relref "/docs/guias/sdk">}}) sobre suas funcionalidades e usos.  

<br>


### **Identificador**

Em nossa modelagem de conta de pagamento, utilizamos dois conceitos para refletir as etapas mencionadas acima: 

|  |   |
| ------- | -------------------------- |
| user_id | Identificador que se refere ao seu perfil na Stone contendo informações cadastrais como nome, sobrenome e CPF ou CNPJ. |
| account_id | Identificador que se refere à sua conta na Stone, contendo dados da sua conta de pagamento. |



