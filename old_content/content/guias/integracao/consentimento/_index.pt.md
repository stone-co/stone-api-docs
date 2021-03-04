---
title: "Consentimento"
date: 2020-05-14T14:47:57-03:00
lastmod: 2020-05-14T14:47:57-03:00
weight: "5"
draft: false
---

###### Como obter acesso às contas de pagamento.

------

Consentimento é o processo em que a usuária dona da conta acessa um link gerado pela Aplicação Parceira e através dele permite o acesso a suas informações e a sua conta de pagamento.

Toda vez que uma Aplicação faz um pedido de consentimento a uma usuária o mesmo englobará todos os escopos que aquela aplicação tem.  No fluxo serão listados para a usuária todos os escopos que estão sendo solicitados.

#### Fluxo de consentimento

Para realizar esse processo, a usuária precisa receber do sistema do parceiro um link que a direcione para uma página da Stone. Nessa página a usuária poderá escolher a quais contas de pagamento ela deseja conceder o acesso. Será necessário que o sistema do parceiro gere esse link, como descrito abaixo. O tempo de expiração do link deve ser de no máximo duas horas.

Caso a usuária **não acesse o link** disponibilizado dentro de seu intervalo de tempo de vida, ele irá expirar. Nesse caso não haverá a concessão do acesso e não será mais possível obtê-la através desse mesmo link, precisando gerar um novo.

Também é possível que a usuária acesse o link mas **não conceda o acesso**, ao escolher a opção *Ignorar*. Nesse caso a usuária será redirecionada para uma página do sistema do parceiro e não será possível para ele operar na conta da usuária.

Havendo a **concessão de acesso**, a usuária será redirecionada para uma página da Aplicação e o parceiro obterá as autorizações necessárias para operar na conta.

O sistema do parceiro será informado do ocorrido para cada um desses três casos.

Observe que no fluxo atual é preciso que o parceiro direcione sua cliente a abrir uma Conta Stone. Quando a usuária estiver com sua Conta Stone aberta, o parceiro poderá realizar o processo de consentimento para operar em sua conta.

#### Gerando um link de consentimento

Uma vez cadastrada e autenticada a Aplicação, a primeira funcionalidade a ser desenvolvida é o consentimento.

Para dar início ao processo de consentimento, basta que a desenvolvedora gere um link com os parâmetros necessários conforme especificados abaixo. Toda a interação com a usuária será gerida pela nossa plataforma.

Após o link ser gerado, ele deverá ser enviado pela Aplicação Parceira para a usuária. Isso pode ser feito por e-mail ou dentro da própria Aplicação como, por exemplo, através de um botão.

#### O link de consentimento deve conter três parâmetros:

1. `client_id`: o ClientID recebido pela desenvolvedora pós-cadastro;
2. `type`: no caso, será sempre o valor "consent";
3. `jwt`: será um token gerado localmente pela desenvolvedora com a mesma chave privada e algoritmo que ela usa para se autenticar. Mais detalhes abaixo.

Com estes parâmetros, basta gerar um link no seguinte formato (por ambiente):

- _Sandbox_: https://sandbox-accounts.openbank.stone.com.br/#/consent?type=consent&amp;client_id=CLIENT_ID&amp;jwt=JWT
- _Produção_: https://accounts.openbank.stone.com.br/#/consent?type=consent&amp;client_id=CLIENT_ID&amp;jwt=JWT

Substituindo CLIENT_ID e JWT por seus respectivos valores.

#### Gerando o token

Gerar um token JWT de consentimento é parecido com o processo de gerar um token de autenticação. O token deve conter os **claims**:

| Campo            | Descrição                                                                                                                                                                                    | Tipo   |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| **Obrigatórios** |                                                                                                                                                                                              |        |
| type             | Será sempre "consent" neste caso.                                                                                                                                                            | String |
| client_id        | Será o ClientID da Aplicação Parceira.                                                                                                                                                       | String |
| redirect_uri     | A URI para redirecionamento após a ação da usuária. **Esta URI foi informada previamente no cadastro da Aplicação Parceira. Caso seja enviada uma URI diferente, retornará erro.**           | String |
| session_metadata | Um objeto que contenha qualquer chave relevante para o parceiro identificar a sessão da usuária. Este valor estará presente na URI de redirecionamento e não pode ser nulo ou um mapa vazio. | Objeto |
| iss              | Usar o client_id da Aplicação.                                                                                                                                                               | String |
| iat              | Momento em que o token foi gerado. É um timestamp UTC. Exemplo: `"iat": 1542235633`.                                                                                                         | Int    |
| aud              | accounts-hubid@openbank.stone.com.br                                                                                                                                                         | String |
| jti              | Identificador único do token gerado. Normalmente se utiliza um UUID.                                                                                                                         | String |
| nbf              | É o momento em que o token passa a ser válido. Na maioria dos casos terá o mesmo valor que `iat` (issued at) pois queremos que ele esteja válido logo a partir do momento de geração.        | Int    |
| exp              | Momento de expiração do token em segundos desde o início da era UNIX (1970). É um timestamp UTC e não pode ser maior que 2 horas. Exemplo: `\"exp\": 1542235633`                             | Int    |


Observe que é preciso **assinar o token JWT com a chave privada da aplicação e o algoritmo RS256**, assim como é feito para o token de [autenticação](https://docs.openbank.stone.com.br/docs/referencia-de-api/autenticacao-guides). Dessa forma, neste token também é preciso incluir um header com as informações sobre o algoritmo de criptografia utilizado, entre outros metadados, como um id da chave utilizada. Por exemplo:

```json5
{
  "alg": "RS256",
  "typ": "JWT"
}
```

{{< notice info >}}
Apesar do ClientID ser o disponibilizado pela Stone ao parceiro no [Cadastro da Aplicação](https://docs.openbank.stone.com.br/docs/cadastro-da-aplicacao-guides) e o mesmo utilizado para montar o token de [autenticação](https://docs.openbank.stone.com.br/docs/referencia-de-api/autenticacao-guides#section-1-gerando-o-token-jwt), observe que o **nome do campo** para esse token é `client_id`, diferente de `clientId` utilizado no token de autenticação.
{{< /notice >}}

Assim, um exemplo de claims para este token seria:

```json5
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

#### Redirect callback

A usuária irá visualizar as permissões às quais a Aplicação Parceira está pedindo acesso e poderá optar por ignorar ou consentir o acesso.

Em ambos os casos, faremos um redirecionamento para a URI cadastrada no token. Acrescentaremos na URI os seguintes campos:
- os valores de session_metadata passados no token;
- a chave "consent_result" que poderá ter o valor de "ignored" ou "approved";
- se o resultado for "approved", também passaremos o campo "resource_id" com o identificador do resource ao qual o consentimento foi dado.

Assim, fica fácil para a desenvolvedora prover uma experiência para ambos os casos: basta validar estes campos!

#### Fluxo para a usuária

Para uma integração [Open Banking](https://docs.openbank.stone.com.br/docs/modelos-de-parceria-guides#section-open-banking) de sucesso é essencial considerar a experiência da usuária, principalmente em fluxos de redirecionamento como para o consentimento. No início desta sessão detalhamos o passo a passo desse procedimento; neste tópico vamos exemplificar algumas das principais telas utilizadas.

Ao seguir o link gerado pela desenvolvedora, a usuária será redirecionada para uma página da Stone. Solicitaremos à dona o acesso à sua conta, explicitando quais permissões ela está concedendo à aplicação parceira. Podemos observar abaixo um exemplo de tela em que isso ocorre.

{{< figure src="https://files.readme.io/e6c6443-consent-1.png" alt="Tela de Consentimento.png">}}

Caso a usuária opte por conceder o acesso no botão `Permitir` e ocorra tudo bem, será exibida uma tela de sucesso, confirmando que a permissão foi concedida. Podemos observar um exemplo dessa tela abaixo.

Ao clicar no botão `Ok, entendi` ela será redirecionada para uma página da aplicação parceira, cujo endereço foi definido no [cadastro da aplicação](https://docs.openbank.stone.com.br/docs/cadastro-da-aplicacao-guides), em Redirect URI.

{{< figure src="https://files.readme.io/58f30d4-preview-chat-tl-consent-aprovado.png" alt="Consentimento aprovado.png">}}

É possível que ocorra também um caso em que a usuária já concedeu o acesso à aplicação parceira. Neste caso, a usuária irá visualizar uma tela como o seguinte exemplo.

Assim como no caso anterior, ela também será redirecionada para uma página da aplicação parceira ao clicar no botão `Ok, entendi`.

{{< figure src="https://files.readme.io/00a5935-tl-com-consentimento.png" alt="Consentimento já concedido.png">}}
