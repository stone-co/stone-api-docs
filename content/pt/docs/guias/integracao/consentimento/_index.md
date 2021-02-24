---
title: "Consentimento"
slug: "consentimento-guides"
hidden: false
createdAt: "2019-05-28T18:05:24.742Z"
updatedAt: "2020-12-29T13:36:51.381Z"
weight: 5
---

Como obter acesso as contas de pagamento.

---

<br>

Consentimento é o processo em que o usuário, dono da conta, acessa um link gerado pela Aplicação Parceira e através dele permite o acesso a suas informações e a sua conta de pagamento.

Toda vez que uma Aplicação faz um pedido de consentimento a um usuário, o mesmo englobará todos os escopos que aquela aplicação tem.  No fluxo serão listados todos os escopos que estão sendo solicitados.




#### **Fluxo de consentimento**


Para realizar esse processo, o usuário precisa receber do sistema do parceiro um link que o direcione para uma página da Stone. Nessa página o usuário poderá escolher a quais contas de pagamento ele deseja conceder o acesso. Será necessário que o sistema do parceiro gere esse link, como descrito abaixo. O tempo de expiração do link deve ser de no máximo duas horas. 

Caso o usuário **não acesse o link** disponibilizado dentro de seu intervalo de tempo de vida, ele irá expirar. Nesse caso não haverá a concessão do acesso e não será mais possível obtê-la através desse mesmo link, precisando gerar um novo. 

Também é possível que o usuário acesse o link mas **não conceda o acesso**, ao escolher a opção *Ignorar*. Nesse caso o usuário será redirecionada para uma página do sistema do parceiro e não será possível para ele operar na conta do usuário. 

Havendo a **concessão de acesso**, o usuário será redirecionada para uma página da Aplicação e o parceiro obterá as autorizações necessárias para operar na conta.

O sistema do parceiro será informado do ocorrido para cada um desses três casos.

Observe que no fluxo atual é preciso que o parceiro direcione seu cliente a abrir uma Conta Stone. Quando o usuário estiver com sua Conta Stone aberta, o parceiro poderá realizar o processo de consentimento para operar em sua conta.




#### **Gerando um link de consentimento**


Uma vez cadastrada e autenticada a Aplicação, a primeira funcionalidade a ser desenvolvida é o consentimento.

Para dar início ao processo de consentimento, basta que o desenvolvedor gere um link com os parâmetros necessários conforme especificados abaixo. Toda a interação com o usuário será gerida pela nossa plataforma.

Após o link ser gerado, ele deverá ser enviado pela Aplicação Parceira para o usuário. Isso deve ser feito dentro da própria Aplicação como, por exemplo, através de um botão. O link de consentimento não deve ser enviado por e-mail para o usuário sob hipótese alguma. 




#### **O link de consentimento deve conter três parâmetros:**

1. `client_id`: o ClientID recebido pela desenvolvedora pós-cadastro;
2. `type`: no caso, será sempre o valor "consent";
3. `jwt`: será um token gerado localmente pela desenvolvedora com a mesma chave privada e algoritmo que ela usa para se autenticar. Mais detalhes abaixo.

Com estes parâmetros, basta gerar um link no seguinte formato (por ambiente):

- _Sandbox_: https://sandbox.conta.stone.com.br/consentimento?client_id=CLIENT_ID&jwt=JWT
- _Produção_: https://conta.stone.com.br/consentimento?client_id=CLIENT_ID&jwt=JWT

Substituindo CLIENT_ID e JWT por seus respectivos valores.



#### **Gerando o token**

Gerar um token JWT de consentimento é parecido com o processo de gerar um token de autenticação. O token deve conter os **claims**:

<br>

| Campo         | Descrição                                       | Tipo                       |
| --------------| ----------------------------------------------- |--------------------------- |
| **Obrigatórios** |  |
| type          | Será sempre "consent" neste caso. | _String_
| clinet_id     | Será o ClientID da Aplicação Parceira. | _String_
| redirect_uri  | A URI para redirecionamento após a ação da usuária. Esta URI foi informada previamente no cadastro da Aplicação Parceira. Caso seja enviada uma URI diferente, retornará erro. | _String_
| session_metadata | Um objeto que contenha qualquer chave relevante para o parceiro identificar a sessão da usuária. Este valor estará presente na URI de redirecionamento e não pode ser nulo ou um mapa vazio. | _Objeto_
| iss           | Usar o client_id da Aplicação. | _String_
| iat           | Momento em que o token foi gerado. É um timestamp UTC. Exemplo: "iat": 1542235633. | _Int_
| aud           | accounts-hubid@openbank.stone.com.br | _String_
| jti           | Identificador único do token gerado. Normalmente se utiliza um UUID. | _String_
| nbf           | É o momento em que o token passa a ser válido. Na maioria dos casos terá o mesmo valor que iat (issued at) pois queremos que ele esteja válido logo a partir do momento de geração. | _Int_
| exp           | Momento de expiração do token em segundos desde o início da era UNIX (1970). É um timestamp UTC e não pode ser maior que 2 horas. Exemplo: "exp": 1542235633 | _Int_

<br>

Observe que é preciso **assinar o token JWT com a chave privada da aplicação e o algoritmo RS256**, assim como é feito para o token de [autenticação](https://docs.openbank.stone.com.br/docs/autenticacao-guides). Dessa forma, neste token também é preciso incluir um header com as informações sobre o algoritmo de criptografia utilizado, entre outros metadados, como um id da chave utilizada. Por exemplo:


```JSON
{
  "alg": "RS256",
  "typ": "JWT"
}
```

{{% pageinfo %}}
**Atenção**

Apesar do ClientID ser o disponibilizado pela Stone ao parceiro no [Cadastro da Aplicação](https://docs.openbank.stone.com.br/docs/cadastro-da-aplicacao-guides) e o mesmo utilizado para montar o token de [autenticação](https://docs.openbank.stone.com.br/docs/autenticacao-guides#section-1-gerando-o-token-jwt), observe que o **nome do campo** para esse token é `client_id`, diferente de `clientId` utilizado no token de autenticação.

{{% /pageinfo %}}


Assim, um exemplo de claims para este token seria:

```JSON
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

<br>

#### **Redirect callback**

o usuário irá visualizar as permissões às quais a Aplicação Parceira está pedindo acesso e poderá optar por ignorar ou consentir o acesso.

Em ambos os casos, faremos um redirecionamento para a URI cadastrada no token. Acrescentaremos na URI os seguintes campos:

<br>

| Chave         | Valor                                           | 
| --------------| ----------------------------------------------- |
| session_metadata | Com os mesmos os valores de passados no token.
| consent_result | Indica o resultado do pedido de consentimento e pode ter os seguintes valores: - "ignored" caso o usuário não dê consentimento, - "approved" caso ele dê o consentimento, - "already_granted" caso o consentimento desse recurso para essa aplicação já tenha sido dado anteriormente.
| resource_id | Identificador do resource ao qual o consentimento foi dado. Só é retornado quando o resultado do consent é "approved".

<br>

{{< alert title="Webhook" >}}
Quando o `consent_result` é `approved` é enviado também o webhook `consent_requested` com os dados do consentimento dado.
{{< /alert >}}


Assim, fica fácil para a desenvolvedora prover uma experiência para ambos os casos: basta validar estes campos!




#### **Fluxo para o usuário**

Para uma integração [Open Banking](https://docs.openbank.stone.com.br/docs/modelos-de-parceria-guides#section-open-banking) de sucesso é essencial considerar a experiência do usuário, principalmente em fluxos de redirecionamento como para o consentimento. No início desta sessão detalhamos o passo a passo desse procedimento; neste tópico vamos exemplificar algumas das principais telas utilizadas.

Ao seguir o link gerado pelo desenvolvedor, o usuário será redirecionado para uma página da Stone. Solicitaremos ao dono o acesso à sua conta, explicitando quais permissões ele está concedendo à aplicação parceira. Podemos observar abaixo um exemplo de tela em que isso ocorre.


![imagem_consentimento](/home/bruno/Documentos/stone-api-docs/content/pt/docs/guias/integracao/consentimento/consentimento.png)


Caso o usuário opte por conceder o acesso no botão `Permitir` e ocorra tudo bem, será exibida uma tela de sucesso, confirmando que a permissão foi concedida. Podemos observar um exemplo dessa tela abaixo.

Ao clicar no botão `Ok, entendi` ele será redirecionado para uma página da aplicação parceira, cujo endereço foi definido no [cadastro da aplicação](https://docs.openbank.stone.com.br/docs/cadastro-da-aplicacao-guides), em Redirect URI.


![imagem_consentimento_aprovado](/home/bruno/Documentos/stone-api-docs/content/pt/docs/guias/integracao/consentimento/consentimento-aprovado.png)


É possível que ocorra também um caso em que o usuário já concedeu o acesso à aplicação parceira. Neste caso, o usuário irá visualizar uma tela como o seguinte exemplo.

Assim como no caso anterior, ele também será redirecionado para uma página da aplicação parceira ao clicar no botão `Ok, entendi`.


![imagem_com_consentimento](/home/bruno/Documentos/stone-api-docs/content/pt/docs/guias/integracao/consentimento/com-consentimento.png)
