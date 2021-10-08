---
title: "TOKEN DE ACESSO"
linkTitle: "TOKEN DE ACESSO"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 2
draft: false
description: >
    
---
<br>

## Overview
---

<br>
Para realizar chamadas na API Stone Open Banking, será necessário ter em mãos um Token de Acesso ou Access Token. 
<br>O Token de Acesso gerado será no formato JWT e funcionará como uma chave de acesso para todas as requisições na API. 

<br>
<br>
O JWT é um padrão (RFC-7519) de mercado que define como transmitir e armazenar objetos JSON de forma compacta e segura entre diferentes aplicações. Os dados nele contidos podem ser validados a qualquer momento, pois o token é assinado digitalmente.

<br>
<br>
Para receber esse Token de Acesso, será necessário que você gere um JWT local, com suas partes em base64 já decodificadas e que deverá ser formado por três seções:

{{< alert >}}
**Header:** é um objeto JSON que define informações sobre o tipo do token (typ) - nesse caso JWT - e o algoritmo de criptografia usado em sua assinatura (alg) - no nosso caso usamos sempre o RS256. 

**Payload:** é um objeto JSON com as Claims (informações/alegações) da entidade tratada. São as informações que o JWT carrega, tipicamente a data de expiração do token ("EXPiration date"), quem gerou aquele token ("ISSuer"), quando ("Instanciated AT"), quem deve consumi-lo ("AUDience") e o que mais for necessário entre as partes — como por exemplo um ID de usuário. Para essa etapa, você precisará de um ClientID, ou seja, o identificador recebido após a realização do [Cadastro da sua Aplicação]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação">}}) com a Stone. <br>Além disso, você deverá preencher as Claims conforme nosso processo de [Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação">}}). 

**Signature:** é a assinatura única de cada token que é gerada a partir de um algoritmo de criptografia e tem seu corpo com base no header, no payload e na chave secreta definida pela aplicação. A assinatura é que vai garantir a integridade do token, se ele foi modificado e se realmente foi gerado por você. Para essa etapa, você já deve ter [gerado um par de chaves]({{< relref "/docs/guias/token-de-acesso/#gerar-chaves-de-acesso">}}). 
{{< /alert >}}


Após a geração do token local formado acima, é preciso fazer uma chamada para o nosso servidor de [Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação">}}) para que a gente faça a validação e retorne o Token de Acesso.

Provido com o Token de Acesso (token que já foi autenticado), você poderá acessar os endpoints da aplicação, que antes estavam restritos. Para realizar esse acesso, é preciso informar esse token no header Authorization da requisição e, por convenção, após a palavra Bearer. 

Em seguida, vamos te guiar para realizar as seguintes etapas para obtenção do seu Token de Acesso:

[Gerar um par de chaves de acesso]({{< relref "/docs/guias/token-de-acesso/#gerar-chaves-de-acesso">}})

[Cadastrar  sua Aplicação]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação">}})

[Fazer a Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação">}})

[Realizar Chamada Autenticada]({{< relref "/docs/guias/token-de-acesso/#chamada-autenticada">}})


<br>

## Gerar Chaves de acesso
---

<br>
Para obter o seu Access Token, será necessário gerar um par de chaves RSA 4096. Você deverá assinar o JWT com a chave privada e nos enviar a chave pública no formato PEM e extensão .pub. <br><br>

Embora existam vários métodos para criação de pares de chaves pública e privada, a ferramenta OpenSSL de código aberto é uma das mais usadas, por isso, recomendamos o seu uso.

Em todas as plataformas disponíveis - Linux, MacOS e Windows, os comandos do OpenSSL são iguais: <br>
```shell
   $ openssl genrsa -out mykey.pem 4096
   $ openssl rsa -in mykey.pem -pubout > mykey.pub
```
Algumas dicas importantes: 

{{< alert >}}
Linux: é uma ferramenta padrão que já vem instalada em quase todas as distribuições.

MacOS: há algumas formas de instalar, sendo o uso da ferramenta “brew” um dos mais simples. 

Windows: é possível adquiri-la através da [Página de Download](https://slproweb.com/products/Win32OpenSSL.html) e obter detalhes sobre o processo de instalação através do [Tutorial de Instalação](https://tecadmin.net/install-openssl-on-windows/). Após a instalação, você deve acrescentar o caminho do programa na variável PATH e adicionar mais uma variável OPENSSL_CONF ao arquivo openssl.cfg, que normalmente vai ser "C:\Program Files\OpenSSL-Win64\bin\openssl.cfg". Atente-se para ajustar o caminho para o local onde você instalou a ferramenta.
{{< /alert >}}

Agora você já pode gerar o seu par de chaves. A chave pública será solicitada pelo nosso time durante a integração. Nós deixamos a chave pública guardada de forma segura e a usaremos para validar o seu token num processo de criptografia assimétrica. <br>**A chave que deverá ser enviada para a Stone através do formulário de integração é sempre a chave pública (arquivo .pub).**<br><br>

**Atenção!**  
<br>Você nunca deve compartilhar a chave privada (arquivo.pem)! A chave privada deve ser armazenada de forma segura por você. <br>Em posse da sua chave privada, qualquer aplicação pode decodificar a assinatura e verificar se ela é válida. <br> Por isso destacamos a importância de manter essa informação em segredo.

Depois de obter seu par de chaves, você está pronto para iniciar conosco o [Cadastro da Aplicação]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação">}}). 

<br>

## Cadastro da Aplicação
---

<br>

Qualquer parceiro ou cliente que deseje acessar e/ou movimentar a sua conta ou de terceiros pela nossa API precisará ter sua aplicação identificada. O identificador que representa a sua aplicação na Stone é chamado ClientID. 

O ClientID será usado no processo de Autenticação, permitindo a identificação da origem dos requests feitos por API. Ou seja, ele será usado no seu Token de Acesso para realizar chamadas. O ClientID é gerado pela Stone, é único e não será alterado posteriormente. 

Para obter um ClientID, você deverá entrar em [contato](https://app.pipefy.com/public/form/Qz4ptt_W/?origem_do_lead=Documenta%C3%A7%C3%A3o) com nosso time comercial. Em seguida, pediremos algumas informações para cadastrar sua aplicação. Nesse formulário, será necessário enviar ao time da Stone:

1. A sua [chave pública]({{< relref "/docs/guias/token-de-acesso/#gerar-chaves-de-acesso">}}) - que será atrelada ao cadastro da sua aplicação.
2. Uma URI de Redirect - precisamos de um local público para redirecionarmos o usuário final depois que ele aprovar ou reprovar o [Consentimento]({{< relref "/docs/guias/consentimento/#overview">}}) de acesso à sua plataforma. Caso você esteja fazendo a integração para acesso à sua própria conta, pode desconsiderar essa etapa. 
3. Uma URI de webhooks - precisamos de um local público para enviar mudanças de estado das contas para aplicações. Essa URI irá receber as informações dos webhooks para seu processamento.
4. Sua linguagem de desenvolvimento - nossa infraestrutura disponibiliza uma API RESTful com respostas em JSON.

Após o recebimento de todas as informações e cadastro da sua aplicação, enviaremos o seu ClientID por e-mail. 

Atenção! O ClientID será enviado para o e-mail identificado no formulário como dono da aplicação. Caso você queira movimentar a sua própria conta, esse e-mail deverá ser o mesmo cadastrado no momento de [abertura da Conta]({{< relref "/docs/guias/conta-de-pagamento/#abertura-de-conta">}}).

Pronto! Com seu ClientID em mãos, você já pode realizar o processo de [Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação">}}). 

<br>

## Autenticação
---


<br>

Para realizar o processo de Autenticação, você deverá enviar uma requisição ao nosso servidor contendo um JWT. O JWT enviado deverá conter as credenciais da sua aplicação ([ClientID]({{< relref "/docs/guias/token-de-acesso/#cadastro-da-aplicação">}}) e deverá ser assinado com a chave privada. Ao receber o request, faremos o processo de validação do token enviado, pois já teremos recebido e armazenado a sua chave pública.

Uma vez que o token seja válido e tenha sido autenticado em nosso servidor, enviaremos como resposta o Access Token, ou seja, o seu Token de Acesso. <br><br>

##### **Padrões utilizados na Autenticação**

Para facilitar ao máximo a integração com nossa API, escolhemos padrões estabelecidos no mercado para realização do processo de autenticação - descritos abaixo. 

**OAuth 2.0** é um padrão de autorização que vai permitir ao usuário conceder acesso limitado a recursos na Conta Stone para aplicações sem a necessidade de expor suas credenciais. Isso significa que o cliente não precisará compartilhar login e senha com ninguém. 

**OpenID Connect** é uma camada de identidade construída em cima do OAuth 2.0 que permite a fácil verificação da identidade do usuário, bem como a capacidade de obter informações básicas de perfil do provedor de identidade - no nosso caso, a Conta Stone. <br><br>

##### **Especificações do JWT para realizar autenticação**

Primeiramente, temos que gerar um token JWT local para conseguir fazer a autenticação com sucesso. Esse token deverá ser preenchido com as claims com os seguintes valores:

| Nome | Valor |
| ---- | ----- |
| exp | Tempo de expiração do token em segundos desde o início da era UNIX (1970). É UTC e não pode ser maior que 15 minutos. Exemplo: "exp": 1542235633 |
| nbf | "Not before", ou seja, data a partir da qual o token é válido. É UTC. Exemplo: "nbf": 1542235633 |
| aud | Quem é a "audiência" deste token. No caso, é o nosso servidor de autenticação. <br>Para o ambiente de Sandbox será: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank. <br>Para Produção será: https://accounts.openbank.stone.com.br/auth/realms/stone_bank |
| realm | Qual é o "reino" dos nossos usuários. Será sempre "stone_bank". |
| sub | O sujeito referente ao token. Deve ser o ClientID enviado ao desenvolvedor após o cadastro da aplicação. |
| clientId | Mesmo valor de sub, ou seja, o ClientID enviado ao desenvolvedor após o cadastro da aplicação. |
| jti | Identificador único do token gerado. Normalmente se utiliza um UUID, mas não é obrigatório usar esse formato desde que a unicidade seja garantida. [Mais informações](https://tools.ietf.org/html/rfc7519#section-4.1.7). |
| iat | Momento em que o token foi gerado. É UTC. Exemplo: "iat": 1542235633 |
| iss | Mesmo valor de sub e clientId, ou seja, o ClientID enviado ao desenvolvedor após o cadastro da aplicação. |

Após gerar esse token localmente, partiremos para receber o access_token e realizar as [chamadas autenticadas]({{< relref "/docs/guias/token-de-acesso/#chamada-autenticada">}}).

O request para receber o access_token é realizado através do método POST com as informações abaixo:
<br><br>

**Header**<br>Na nossa API, usaremos sempre o algoritmo **RS256**. Esse algoritmo especificado nessa RFC usa criptografia “RSASSA-PKCS1-v1_5 com SHA-256”. 
Abaixo você encontrará um exemplo de header.

```json
{
  "alg": "RS256",
  "typ": "JWT"
}
```

A chamada é com o método **POST**, com os headers **Content-Type** e **User-Agent**. <br>O **Content-Type** informado deve ser **x-www-form-urlencoded** (o mesmo usado por submissão de formulários HTML) e o header **User-Agent** deve estar habilitado com o nome da sua aplicação. Verifique o exemplo abaixo:

```json
{
  "user-agent": "Nome da aplicação",
  "content-type": "application/x-www-form-urlencoded"
}
```
<br>

**Payload** <br>É um objeto JSON que trará as informações que usaremos para verificar a autenticidade da chamada e retornar o Token de Acesso. É necessário enviar o campo `client_id`, o campo `grant_type`, que será um campo de valor fixo (**client_credentials**), o campo `client_assertion`, que será o token gerado localmente citado acima, e por último o campo `client_assertion_type`, que também terá seu valor fixo (**urn:ietf:params:oauth:client-assertion-type:jwt-bearer**), fechando o fluxo de client credentials para o servidor.

<br>
Esse request deverá ser realizado nas seguintes URLs (por ambiente):
<br><br>

| Ambiente | Endpoint de Acesso |
| -------- | ------------------ |
| Sandbox | https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token |
| Produção | https://accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token |



Você deverá receber como resposta um JSON com uma chave, ou seja, o seu Token de Acesso, que permitirá que você faça [Chamadas Autenticadas]({{< relref "/docs/guias/token-de-acesso/#chamada-autenticada">}}).


<br>

## Chamada autenticada
---



Após realizar o processo de [Autenticação]({{< relref "/docs/guias/token-de-acesso/#autenticação">}}) e receber como resposta o seu Token de Acesso, basta colocá-lo no header Authorization. Você irá usar o valor recebido para preenchimento do Bearer ACCESS_TOKEN de todas as chamadas realizadas em nossa API.

Além do Token de acesso, é necessário preencher sempre no header o campo **User-Agent**, que deve estar habilitado com o nome da sua aplicação.

Para realizar chamadas autenticadas em nossa API, disponibilizamos as seguintes URLs: <br><br>


| Ambiente | Endpoint de Acesso |
| -------- | ------------------ |
| Sandbox | https://sandbox-api.openbank.stone.com.br |
| Produção | https://api.openbank.stone.com.br |


{{% pageinfo %}}
**Não solicite um token por chamada!**

O access_token possui duração de 15 minutos e você deve utilizar esse mesmo token durante todo seu período de utilização, não importa quais e quantas chamadas diferentes sua aplicação irá fazer nesse período.

{{% /pageinfo %}}


A seguir, vamos te guiar pela seção [Conta de Pagamento]({{< relref "/docs/guias/conta-de-pagamento">}}), onde você poderá entender mais sobre as características do nosso negócio e sobre o processo de abertura de conta.


## Collection do Postman
---

Para ajudar na realização das chamadas autenticadas, disponibilizamos alguns endpoints e códigos prontos!

Você pode baixar clicando nos links abaixo:

- <a href="link-para-consentimento.zip" download="Link de consentimento">Código em JS para geração do link de consentimento</a>
- <a href="get_token_p parceiros.zip" download="Token de autenticação">Código em Python para geração do token de autenticação</a>
- <a href="Criar-conta-Stone.zip" download="Criação de conta">Código em Python para pedido de criação para contas Stone</a>
- <a href="Criar_Pagamentos.zip" download="Criar_Pagamentos">Collection do Postman para criar Pagamentos</a>
- <a href="Pix_out.zip" download="Pix_out">Collection do Postman para realização de Pix</a>
- <a href="Transferencias.zip" download="Transferências">Collection do Postman para Transferências</a>
- <a href="Dados_da_Conta.zip" download="Dados da Conta">Collection do Postman para Dados da Conta (inclui extrato)</a>
- <a href="Simulacoes(dry-run).zip" download="Dry-run">Collection do Postman para Simulações(Dry-run)</a>
- <a href="Comprovantes.zip" download="Comprovantes">Collection do Postman para emissão de Comprovantes</a>
- <a href="Link_de_pagamento.zip" download="Link de Pagamento">Collection do Postman para Link de Pagamento</a>
- <a href="Recargas.zip" download="Recargas">Collection do Postman para Recargas</a>
- <a href="Boletos.zip" download="Boletos">Collection do Postman para Boletos</a>
