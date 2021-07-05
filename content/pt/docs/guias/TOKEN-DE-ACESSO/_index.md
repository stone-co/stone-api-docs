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

### Overview
---

<br>
Para realizar chamadas na API Stone Open Banking, será necessário ter em mãos um Token de Acesso, ou Access Token. 
<br>O Token de Acesso gerado será no formato JWT e funcionará como uma chave de acesso para todas as requisições na API. 

<br>
<br>
O JWT é um padrão (RFC-7519) de mercado que define como transmitir e armazenar objetos JSON de forma compacta e segura entre diferentes aplicações. Os dados nele contidos podem ser validados a qualquer momento pois o token é assinado digitalmente.

<br>
<br>
Para receber esse Token de Acesso, será necessário que você gere um  JWT local, com suas partes em base64 já decodificadas e que deverá ser formado por três seções:

{{< alert >}}
Header: é um objeto JSON que define informações sobre o tipo do token (typ) - nesse caso JWT - e o algoritmo de criptografia usado em sua assinatura (alg) - no nosso caso usamos sempre o RS256. 

Payload: é um objeto JSON com as Claims (informações /alegações) da entidade tratada. São as informações que o JWT carrega, tipicamente a data de expiração do token ("EXPiration date"), quem gerou aquele token ("ISSuer"), quando ("Instanciated AT"), quem deve consumi-lo ("AUDience"), e o que mais for necessário entre as partes — como por exemplo um ID de usuário. Para esta etapa, você precisará de um ClientID, ou seja, o identificador recebido após realização do [Cadastro da sua Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/) com a Stone. <br>Além disso, você deverá preencher os Claims conforme nosso processo de [Autenticação](/docs/guias/token-de-acesso/autenticacao/). 

Signature: É a assinatura única de cada token que é gerada a partir de um algoritmo de criptografia e tem seu corpo com base no header, no payload e na chave secreta definida pela aplicação. A assinatura é que vai garantir a integridade do token, se ele foi modificado e se realmente foi gerado por você. Para essa etapa, você já deve ter [gerado um par de chaves](/docs/guias/token-de-acesso/gerar-chaves-de-acesso/). 
{{< /alert >}}


Após a geração do token local formado acima, é preciso fazer uma chamada para o nosso servidor de [Autenticação](/docs/guias/token-de-acesso/autenticacao/) para que a gente faça a validação e retorne o Token de Acesso.

Provido com o Token de Acesso (token que já foi autenticado), você poderá acessar os endpoints da aplicação, que antes estavam restritos. Para realizar esse acesso, é preciso informar esse token no header Authorization da requisição e, por convenção, após a palavra Bearer. 

Em seguida, vamos te guiar para realizar as seguintes etapas para obtenção do seu Token de Acesso:

[Gerar um par de chaves de acesso](/docs/guias/token-de-acesso/gerar-chaves-de-acesso/)

[Cadastrar  sua Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/)

[Fazer a Autenticação](/docs/guias/token-de-acesso/autenticacao/)

[Realizar Chamada Autenticada](/docs/guias/token-de-acesso/chamada-autenticada/)


<br>

### Gerar Chaves de acesso
---

<br>
Para obter o seu Access Token, será necessário gerar um par de chaves RSA 4096. Você deverá assinar o JWT com a chave privada e nos enviar a chave pública no formato PEM e extensão .pub. <br><br>

Embora existam vários métodos para criação de pares de chaves público e privada, a ferramenta OpenSSL de código aberto é uma das mais usadas, por isso, recomendamos o seu uso.

Em todas as plataformas disponíveis - Linux, MacOS e Windows, os comandos do OpenSSL são iguais: <br>

    openssl genrsa -out mykey.pem 4096
    openssl rsa -in mykey.pem -pubout > mykey.pub

Algumas dicas importantes: 

{{< alert >}}
Linux: é uma ferramenta padrão que já vem instalada em quase todas as distribuições.

MacOS: há algumas formas de instalar, sendo o uso da ferramenta “brew” um dos mais simples. 

Windows: É possível adquirí-la através da [Página de Download](https://slproweb.com/products/Win32OpenSSL.html), e obter detalhes sobre o processo de instalação através do [Tutorial de Instalação](https://tecadmin.net/install-openssl-on-windows/). Após a instalação, você deve acrescentar o caminho do programa na variável PATH e adicionar mais uma variável OPENSSL_CONF para o arquivo openssl.cfg, que normalmente vai ser C:\Program Files\OpenSSL-Win64\bin\openssl.cfg. Atente-se para ajustar o caminho para o local onde você instalou a ferramenta.
{{< /alert >}}

Agora você já pode gerar o seu par de chaves. A chave pública será solicitada pelo nosso time durante a integração. Nós deixamos a chave pública guardada de forma segura e usaremos para validar o seu token num processo de criptografia assimétrica. A chave que deverá ser enviada para Stone através do formulário de integração é sempre a chave pública (arquivo .pub).<br><br>

**Atenção!**  
<br>Você nunca deve compartilhar a chave privada (arquivo.pem)! A chave privada deve ser armazenada de forma segura por você. <br>Em posse da sua chave privada, qualquer aplicação pode decodificar a assinatura e verificar se ela é válida. <br> Por isso destacamos a importância de manter essa informação em segredo.

Depois de obter seu par de chaves, você está pronto para iniciar conosco o [Cadastro da Aplicação](/docs/guias/token-de-acesso/cadastro-da-aplicacao/). 

<br>

### Cadastro da Aplicação
---

<br>

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

<br>

### Autenticação
---

<br>

<br>

Para realizar o processo de Autenticação, você deverá enviar uma requisição ao nosso servidor contendo um JWT. O JWT enviado deverá conter as credenciais da sua aplicação ([ClientID](/docs/guias/token-de-acesso/cadastro-da-aplicacao/)) e deverá ser assinado com a chave privada. Ao receber o request, faremos o processo de validação do token enviado, pois já teremos recebido e armazenado a sua chave pública.

Uma vez que o token seja válido e tenha sido autenticado em nosso servidor, enviaremos como resposta o Access Token, ou seja, o seu Token de Acesso. <br><br>

##### **Padrões utilizados na Autenticação**

Para facilitar ao máximo a integração com nossa API, escolhemos padrões estabelecidos no mercado para realização do processo de autenticação - descritos abaixo. 

**OAuth 2.0** é um padrão de autorização que vai permitir ao usuário conceder acesso limitado a recursos na Conta Stone para Aplicações sem a necessidade de expor suas credenciais. Isso significa que o cliente não precisará compartilhar login e senha com ninguém. 

**OpenID Connect** é uma camada de identidade construída em cima do OAuth 2.0 que permite a fácil verificação da identidade do usuário, bem como a capacidade de obter informações básicas de perfil do provedor de identidade - no nosso caso, a Conta Stone. <br><br>

##### **Especificações do JWT para realizar autenticação**

A [chamada](/docs/guias/token-de-acesso/chamada-autenticada/) é realizada através do método POST com as informações abaixo:

**Header**<br>Na nossa API, usaremos sempre o algoritmo RS256. Este algoritmo especificado nesta RFC usa criptografia “RSASSA-PKCS1-v1_5 com SHA-256”. 
Abaixo você encontrará um exemplo de header.

```JSON
{
  "alg": "RS256",
  "typ": "JWT"
}
```

A chamada é com o método POST com o header Content-Type e User-Agent. <br>O Content-Type informado deve ser x-www-form-urlencoded (o mesmo usado por submissão de formulários HTML) e o header User-Agent deve estar habilitado. Verifique o exemplo abaixo:

```JSON
{
  "user-agent": "Nome da aplicação",
  "content-type": "application/x-www-form-urlencoded"
}
```
<br>

**Payload** <br>É um objeto JSON que trará as informações que usaremos para verificar a autenticidade da chamada e retornar o Token de acesso. É necessário enviar o campo ClientID, o campo  grant_type que será um campo de valor fixo (client_credentials), o campo `client_assertion` que será o token gerado localmente citado acima e por último o campo `client_assertion_type` que também terá seu valor fixo (urn:ietf:params:oauth:client-assertion-type:jwt-bearer), fechando o fluxo de client credentials para o servidor.

Para conseguir se autenticar com sucesso, você deverá preencher os claims com os seguintes valores:

| Nome | Valor |
| ---- | ----- |
| exp | Tempo de expiração do token em segundos desde o início da era UNIX (1970). É UTC e não pode ser maior que 15 min. Ex: "exp": 1542235633 |
| nbf | "Not before", ou seja, data a partir da qual o token é válido. É UTC. Ex: "nbf": 1542235633 |
| aud | Quem é a "audiência" deste token. No caso, é o nosso servidor de autenticação. <br>Para o ambiente de Sandbox será: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank . <br>Para Produção será: https://accounts.openbank.stone.com.br/auth/realms/stone_bank |
| realm | Qual é o "reino" das nossos usuários. Será sempre "stone_bank". |
| sub | O sujeito referente ao token. Deve ser o ClientID enviado ao desenvolvedor pós-cadastro da Aplicação. |
| clientId | Mesmo valor de sub, ou seja, o ClientID enviado ao desenvolvedor pós-cadastro da Aplicação. |
| jti | Identificador único do token gerado. Normalmente se utiliza um UUID, mas não é obrigatório usar esse formato desde que a unicidade seja garantida. [Mais informações](https://tools.ietf.org/html/rfc7519#section-4.1.7) |
| iat | Momento em que o token foi gerado. É UTC. Ex. "iat": 1542235633 |

<br>
<br>
Esta chamada deverá ser realizada nas seguintes URLs (por ambiente):
<br><br>

| Ambiente | Endpoint de Acesso |
| -------- | ------------------ |
| Sandbox | https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token |
| Produção | https://accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token |



Você deverá receber como resposta um JSON com uma chave, ou seja, o seu Token de Acesso, que permitirá que você faça [Chamadas Autenticadas](/docs/guias/token-de-acesso/chamada-autenticada/).


<br>

### Chamada autenticada
---

<br>

Após realizar o processo de [Autenticação](/docs/guias/token-de-acesso/autenticacao/) e receber como resposta o seu Token de Acesso, basta colocá-lo no header Authorization. Você irá usar o valor recebido para preenchimento do  Bearer ACCESS_TOKEN.

Para realizar chamadas autenticadas em nossa API, disponibilizamos as seguintes URLs: <br><br>


| Ambiente | Endpoint de Acesso |
| -------- | ------------------ |
| Sandbox | https://sandbox-api.openbank.stone.com.br |
| Produção | https://api.openbank.stone.com.br |


{{% pageinfo %}}
**Não solicite um token por chamada!**

O access_token possui duração de 15 minutos e você deve utilizar esse mesmo token durante todo seu período de utilização, não importa quais e quantas chamadas diferentes sua aplicação irá fazer nesse período.

{{% /pageinfo %}}


A seguir, vamos te guiar pela seção [Conta de Pagamento](/docs/guias/conta-de-pagamento/), onde você poderá entender mais sobre as características do nosso negócio e sobre o processo de abertura de conta.


