---
title: "Conta Stone SDK"
slug: "conta-stone-sdk"
hidden: false
date: "2019-11-19T14:32:50.860Z"
lastmod: "2019-11-19T22:48:16.424Z"
---


<br>

Sejam bem-vindos à documentação da Conta Stone SDK. Através da Conta Stone SDK é possível fazer o processo de abertura de conta e login no Stone OpenBank.



---


#### **Introdução**


A Conta Stone SDK é o ponto de entrada para acesso às nossas SDKs de autenticação (Auth SDK), aprovação (Approver SDK) e verificação de [KYC](https://en.wikipedia.org/wiki/Know_your_customer) (_Know your costumer_) (Pegasus SDK). Segue abaixo um diagrama de como funciona a comunicação entre esses três atores.


![imagem_conta_stone_sdk_diagram](/docs/guias/conta-stone-sdk/conta-stone-sdk-diagram.png)


- Auth SDK - responsável por executar todo o processo de autenticação seguindo as diretrizes do [oAuth2](https://oauth.net/2/).

- Approver SDK - realiza todo o processo de aprovação e rejeição de transações.

- Pegasus SDK - SDK de KYC, responsável por capturar as informações do usuário que está realizando cadastro na conta.


<br>


#### **Como integrar com a SDK**


Antes de começar a integração é necessário obter uma chave de acesso ao nosso repositório. Para obter esta chave, entre em contato com a gente. 

No arquivo `build.gradle` do projeto, adicione a URL do repositório.

```
maven { url "https://packagecloud.io/priv/${access-key}/Stone/stoneid/maven2"}
```

Importe a dependência da Conta Stone SDK

```
implementation 'co.stone:conta:${latest_version}'
```

Sincronize o projeto e pronto! Já é possível utilizar a conta-stone-sdk.

<br>

#### **Inicializando a SDK**


Uma vez que a dependência foi importada o passo seguinte da integração é inicializar a SDK no seu app, para isso é necessário especificar os parâmetros abaixo.

```
ContaStone.initialize(
            application = applicationContext,
            environment = Environment.Production,
            appInfo = AppInfo(
                name = "Conta Stone Android",
                version = BuildConfig.VERSION_NAME,
                buildId = BuildConfig.BUILD_ID
            ),
            clientId = "client_id",
            redirectUri = URI("br.com.stone.openbank.example:/oauth2redirect"),
            authFlowUIConfig = AuthFlowUIConfig(R.style.AppTheme),
            httpClientConfig = HttpClientConfig(interceptors = emptyList()),
            tokenKeyMasterUri =  URI("android-keystore://my-app"),
            userBlockedActions = UserBlockedIntentConfig(
                uriLogout = "myapp://mobile.example.logout",
                uriChat = "myapp://mobile.example.chat"
            )
        )
```

`application`: Trata-se da instância do Application do seu app.

`environment`: Existem 3 ambientes para os quais a sdk pode apontar: `Homolog`, `Sandbox` e `Production`.

`appInfo`: Informações referentes ao app como nome, versão e build.

`client_id`: Identificador fornecido pelo time de suporte OpenBank.

`redirect_uri`: URL de redirecionamento para o app.

`authFlowUIConfig`: Com esta configuração é possível passar o tema da sua aplicação para a SDK. Assim, as cores principais do estilo do seu app serão aplicadas nas telas internas da SDK.

`httpClientConfig`: Trata-se de configurações HTTP customizadas, como `interceptors`, `connectionTimeoutMs`, `readTimeoutMs`, `writeTimeoutMs`, `networkInterceptors`.

`tokenKeyMasterUri`: Uma URI para a chave-mestra no formato `android-keystore://`. Essa chave será utilizada para acessar o Keystore do android e salvar o token da usuária de forma segura. 

`userBlockedActions`: Se um determinado usuário errar a senha de 6 dígitos mais de x vezes, ele será temporariamente bloqueado. Neste momento será exibida uma tela com duas opções: acesso ao canal de relacionamento ou fazer logout. Ao escolher entre elas, o usuário é redirecionado de volta para o app, através dessas duas URIs.

Para mais detalhes sobre como configurar deep link no seu app, clique  [aqui](https://developer.android.com/training/app-links/deep-linking). 


<br>

#### **Autenticação e verificação de KYC**


Para iniciar o fluxo é necessário seguir o método abaixo:

```
fun startAuthAndVerificationFlowForResult(
        activity: Activity,
        requestCode: Int,
        request: AuthFlowRequest,
        params: VerificationParams
    )
```

O atributo `request` refere-se a informações customizadas para o login, como os `scopes`. Tais recursos estarão disponíveis para o usuário ao chamar algum dos endpoints do serviço. Já o `loginHint` salva o email do usuário e é usado para preencher o username na tela de login.

O atributo `params` recebe comandos de dois tipos: o modo de inicialização, ou seja, a maneira como o fluxo deve ser iniciado; e o `NotificationRegister`, que contém o token do Firebase Cloud Message do usuário logado para que seja registrado no serviço de notificações. Os modos de inicialização que podem ser escolhidos são:

`StartingApp` - Inicia todo o fluxo de autenticação e checkagem de KYC.

`AccountSelectionRequest` - Exibe a tela de troca de conta e lida com a escolha do usuário. 

`PushNotificationReceived` - Deve ser iniciado ao receber uma notificação de abertura de conta referente ao processo de abertura de conta.

`NewAccountCreated` - Chamado de verificação de pendência a cada conta aberta pelo app/sistema. 

Este método executa os fluxos internos de autenticação e verificação de KYC. Quando o processo é finalizado, a `conta-stone-sdk` retorna um resultado que será tratado pelo app.

<br>


#### **Lidando com o resultado da sdk**


Ao finalizar o fluxo de autenticação e verificação a SDK emite um resultado para o app informando o desfecho do fluxo. Segue abaixo um exemplo de como tratar o resultado emitido pela `conta-stone-sdk` e o que cada um significa:

```
  override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)

        when (requestCode) {
            AUTH_AND_VERIFICATION_RC -> {
                val result = contaStone.parseAuthAndVerificationResult(data)

                when (result) {
                    is AuthAndVerificationResult.Ok -> toast("Success")
                    is AuthAndVerificationResult.MissingData -> toast("Some error occur while reading data")
                    is AuthAndVerificationResult.UserCancelled -> toast("User cancelled flow")
                    is AuthAndVerificationResult.ReturnToPreviousScreen -> toast("Returned to the previous screen and was logged out")
                    is AuthAndVerificationResult.UserLoggedOut -> toast("User logged out")
                    is AuthAndVerificationResult.BlockedUser -> toast("This user is blocked")
                    is AuthAndVerificationResult.Error -> toast("Some error occur during auth and check flow)
                }
            }
        }
    }
```

<br>

#### **Como fazer logout do usuário**


Como mencionado anteriormente, a `conta-stone-sdk` se comunica com a sdk de autenticação, que pode ser acessada pelo método `contaStone.auth()` e permite acesso aos métodos da interface da authSdk, como o método de logout. Confira abaixo um exemplo de como isso funciona:

```
contaStone.auth().logout { exception: AuthFlowException? ->
                        exception?.let { toast(" Success ")} ?: toast("Erro during logout")
                    }
```
Quando a resposta é nula, o logout ocorreu com sucesso. Quando não, algum erro ocorreu durante o fluxo.

<br>

#### **Cliente autenticado**

A authSDK é responsável por todo o processo de autenticação, incluindo a adição do token no header das chamadas até a api do Stone Openbank. Para realizar tudo isso, a SDK cria um client e adiciona um interceptor, o qual recupera o token do storage e o adiciona no header da chamada.

Esse client possui certificate pinning com os certificados da api do Stone OpenBank e é possível acessá-lo chamando o método `contaStone.auth().client()`, o qual retorna um `OkHttpClient` e pode ser utilizado nas chamadas HTTP do seu app.
