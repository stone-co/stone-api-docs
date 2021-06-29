---
title: "Autenticação"
linkTitle: "Autenticação"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 4
draft: false
description: >

---
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
