---
title: "Gerando um Link de Consentimento"
linkTitle: "Gerando um Link de Consentimento"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 3
draft: true
description: >

---
<br>

Após cadastrar e autenticar a sua aplicação, você está apto a pedir consentimento aos seus clientes que tenham realizado a abertura de uma conta Stone. Ressaltamos que toda interação com o usuário neste processo será gerida por nossa plataforma. 

Seguindo os parâmetros descritos abaixo, você deverá enviar o link ao usuário por meio da sua aplicação. 
<br>O link de consentimento deve ser enviado dentro da própria aplicação. Você pode, por exemplo, disponibilizar um botão em sua plataforma para que o usuário acesse o link. Este link não deve ser enviado ao usuário por e-mail sob hipótese alguma.

<br>

##### **Parâmetros do link de consentimento**

O link de consentimento deverá conter três parâmetros:
- client_id: o ClientID recebido pelo desenvolvedor pós-cadastro;
- type: no caso, será sempre o valor “consent”;
- jwt: será um token gerado localmente pelo desenvolvedor com a mesma chave privada e algoritmo que ele usa para se autenticar. Mais detalhes abaixo.

Com estes parâmetros, basta gerar um link no seguinte formato (por ambiente), substituindo CLIENT_ID e JWT por seus respectivos valores:

|   |   |
| - | - | 
| Sandbox | https://sandbox.conta.stone.com.br/consentimento?client_id=CLIENT_ID&jwt=JWT |
| Produção | https://conta.stone.com.br/consentimento?client_id=CLIENT_ID&jwt=JWT |

<br>


Assim como fizemos o processo de gerar um Token de Acesso autenticado, também será gerado um JWT para pedido do Consentimento. 

<br>

##### **Especificações do JWT para pedir consentimento**

<br>

**Header**
<br>Observe que é preciso assinar o token JWT com a chave privada da aplicação e o algoritmo RS256, assim como é feito para o token de autenticação. Dessa forma, neste token também é preciso incluir um header com as informações sobre o algoritmo de criptografia utilizado, entre outros metadados, como um id da chave utilizada. Por exemplo:

```json
{
  "alg": "RS256",
  "typ": "JWT"
}
```

<br>

**Payload**
<br>O token deve conter os claims abaixo:

| Campos  **Obrigatórios**   | Descrição        | Tipo           |
| ---------------- | ---------------- | -------------- |
| type             | Será sempre "consent" neste caso.    | _String_ |
| client_id        | Será o ClientID da Aplicação Parceira.  | _String_ |
| redirect_uri     | A URI para redirecionamento após a ação do usuário. Esta URI foi informada previamente no cadastro da Aplicação Parceira. Caso seja enviada uma URI diferente, retornará erro.  | _String_ |
| session_metadata | Um objeto que contenha qualquer chave relevante para o parceiro identificar a sessão do usuário. Este valor estará presente na URI de redirecionamento e não pode ser nulo ou um mapa vazio. | _Objeto_ |
| iss              | Usar o client_id da Aplicação.   | _String_ |
| iat              | Momento em que o token foi gerado. É um timestamp UTC. Exemplo: "iat": 1542235633.   | _Int_    |
| aud              | accounts-hubid@openbank.stone.com.br   | _String_ |
| jti              | Identificador único do token gerado. Normalmente se utiliza um UUID.     | _String_ |
| nbf              | É o momento em que o token passa a ser válido. Na maioria dos casos terá o mesmo valor que iat (issued at) pois queremos que ele esteja válido logo a partir do momento de geração.          | _Int_    |
| exp              | Momento de expiração do token em segundos desde o início da era UNIX (1970). É um timestamp UTC e não pode ser maior que 2 horas. Exemplo: "exp": 1542235633   | _Int_    |

<br>

Segue um exemplo de como ficariam os claims preenchidos: 

<br>

```json
{
  "type": "consent",
  "client_id": "MY CLIENT ID", 
  "iss": "MY CLIENT ID",
  "redirect_uri": "https://mypreviouslyregistereduri.com",
  "session_metadata": {
    "user_session": "xxxxxxxxxxxxxxxxxxxxx",
  },
  "iat": 1542235633,
  "nbf": 1542235633,
  "exp": 1549069563,
    "jti": "41e8aa9f-bb9c-4fd2-9953-2595dbbd5a83",
  "aud": "accounts-hubid@openbank.stone.com.br"
}
```
