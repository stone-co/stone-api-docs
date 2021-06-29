---
title: "Fluxo de consentimento"
linkTitle: "Fluxo de consentimento"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 2
draft: false
description: >

---
<br>

A partir da abertura de conta realizada pelo usuário, uma plataforma poderá solicitar acesso ao compartilhamento de informações e iniciação de pagamentos na conta de um usuário. Para isso, deverá gerar um **Link de Consentimento** dentro do padrão estabelecido. 

Após gerar e enviar o Link ao usuário, poderão acontecer três situações, das quais o parceiro será notificado:

###### **<ins>Usuário acessa o link e dá consentimento ao parceiro</ins>**

Ao acessar o link, o usuário será direcionado para um página da Stone em que irá escolher a quais contas de pagamento ele deseja conceder acesso ao parceiro. Ele também poderá verificar a quais escopos o parceiro passará a ter acesso após dar consentimento. Uma vez dado o consentimento, o usuário deverá ser direcionado de volta a uma página do parceiro. 

Veja abaixo um exemplo da tela de pedido de consentimento que será disponibilizada ao cliente:

![solicitacao-consentimento](/docs/guias/CONSENTIMENTO/Fluxo-de-consentimento/solicitacao-de-consentimento.png)

<br>
Veja abaixo um exemplo de permissão concedida:

![consentimento-aprovado](/docs/guias/CONSENTIMENTO/Fluxo-de-consentimento/consentimento-aprovado.png)

<br>Ao clicar no botão "Ok, entendi" o usuário será redirecionado para uma página da aplicação parceira, cujo endereço foi definido no [Cadastro da Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/).

<br>

###### **<ins>Usuário acessa o link e não dá consentimento ao parceiro</ins>**

<br>

Pode acontecer também o caso em que o usuário rejeitar o consentimento solicitado. Neste caso, ele será redirecionado a uma página do parceiro. O parceiro, neste caso, não poderá acessar informações nem operar a conta do usuário. 



**Atenção!** <br>Em ambos os casos citados acima, faremos um redirecionamento para a URI cadastrada no token. Acrescentaremos na URI os seguintes campos: 

<br>

| Chave | Valor |
| ----- | ----- | 
| session_metadata | Com os mesmos os valores de passados no token. |
| consent_result | Indica o resultado do pedido de consentimento e pode ter os seguintes valores:<br>- `ignored`: caso o usuário não dê consentimento;<br>- `approved`: caso ele dê o consentimento e<br>- `already_granted`: caso o consentimento desse recurso para essa aplicação já tenha sido dado anteriormente. | 
| resource_id | Identificador do resource ao qual o consentimento foi dado. Só é retornado quando o resultado do consent é `approved`. |

<br>

Quando o consent_result é `approved` é enviado também o webhook consent_requested com os dados do consentimento dado. Dessa forma, você poderá prover uma experiência fluída para ambos os casos, basta validar estes campos! 

<br>

###### **<ins>Usuário ignora o link </ins>**

<br>

O link de consentimento tem validade de 2 horas após a sua geração. Caso o usuário não acesse o mesmo dentro desse período, será necessário gerar um novo link e fazer um novo envio. 

