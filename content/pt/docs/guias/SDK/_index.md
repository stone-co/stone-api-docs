---
title: "SDK"
linkTitle: "SDK"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-06-28T09:00:00-03:00
weight: 7
draft: false
description: >

---

<br>

## Overview
---
<br>

SDK é a abreviação de Software Development Kit ou, em português, Kit de Desenvolvimento de Software. Um SDK é um conjunto de ferramentas de desenvolvimento de software capaz de facilitar a integração de sistemas em diferentes linguagens de programação. Além disso, usando um SDK é possível ter mais segurança e confiabilidade no processo de integração. 

Construímos a Conta Stone SDK com o objetivo de permitir que parceiros como plataformas e ERPs possam realizar o processo de abertura de conta Stone sem que seus usuários tenham que fazer o download do nosso aplicativo (iOS e Android). 
<br>Assim, de maneira segura, os usuários poderão realizar os processo de autenticação e KYC interagindo de maneira direta com a Stone, mas por meio da SDK integrada pelo parceiro. 

A Conta Stone SDK funciona como ponto de entrada para os três processos abaixo:
- SDK de Autenticação (Auth SDK): Responsável por executar o processo de Autenticação seguindo os padrões especificados.
- Verificação  de KYC (Pegasus SDK):  Responsável por capturar as informações do usuário que está realizando cadastro na conta.

[//]: <> (Aprovação (Approver SDK): Responsável por realizar aprovações ou reprovações de transações)

Após obter o seu [Token de Acesso]({{< relref "/docs/guias/token-de-acesso">}}), caso deseje usar nossa SDK e disponibilizar as etapas acima descritas aos seus usuários, siga os próximos passos para instalação do kit para [iOS]({{< relref "/docs/guias/sdk/#integração-ios">}}) e [Android]({{< relref "/docs/guias/sdk/#integração-android" >}}).

<br>

## Integração Android
---
<br>

A Conta Stone SDK é responsável por todo o fluxo de login e Know Your Customer da [Stone Openbank API](/docs/guias/stone-open-banking/overview/).


##### **Contato**
---

Se durante a integração encontrar algum problema ou ponto de melhoria entre em contato com a gente através da ferramenta de suporte.



##### **Como funciona**
---

A Conta Stone SDK é o ponto de entrada para acesso às nossas SDKs de autenticação, aprovação e verificação de [KYC](https://en.wikipedia.org/wiki/Know_your_customer) (*Know your constumer*).

 - A SDK de autenticação é responsável por executar todo o processo de autenticação seguindo as diretrizes do [oAuth2](https://oauth.net/2/).

 - A SDK de aprovação é responsável pelo processo de aprovação e rejeição de transações.

 - A SDK de KYC é responsável por capturar as informações do usuário que está realizando cadastro na conta.

<br>

##### **Como Integrar com a Conta Stone SDk**
---

Antes de começar a integração é necessário obter uma chave de acesso ao repositório, pois trata-se de um repositório privado. Para obter esta chave entre em contato com a gente.

No arquivo `build.gradle` do projeto adicione a URL do repositório e substitua o `{access-key}` pela chave fornecida.

```python
maven { url "https://packagecloud.io/priv/${access-key}/Stone/stoneid/maven2"}
```

Também é preciso adicionar o Jetpack, pois usamos algumas libs que estão disponíveis neste repositório.

```python
maven { url 'https://jitpack.io' }
```

Importe a dependência da Conta Stone SDK.

```python
implementation 'co.stone:conta:${latest_version}'
```

A Conta Stone SDK utiliza o Firebase para implementar alguns de seus serviços, logo é necessário ter um projeto no firebase e integrá-lo no seu app. Para mais informações sobre como adicionar o Firebase ao seu projeto acesse este [link](https://firebase.google.com/docs/android/setup).

Sincronize o projeto e pronto, já é possível utilizar a Conta Stone SDK!

<br>

##### **Inicializando a SDK**
---

Uma vez que a dependência foi importada o passo seguinte da integração é inicializar a SDK no seu app, para isso é necessário especificar os parâmetros abaixo.

```python
private val environment = Environment.Sandbox

 ContaStone.initialize(
            application = application,
            environment = environment,
            appInfo = AppInfo(
                name = "Conta Stone Sample App",
                applicationId = BuildConfig.APPLICATION_ID,
                buildId = BuildConfig.BUILD_TYPE,
                version = BuildConfig.VERSION_NAME
            ),
            authFlowUIConfig = AuthFlowUIConfig(themeId = R.style.Theme_ContaStoneSdkSample),
            clientId = "myapp@example.com.br",
            deepLinkUris = DeepLinkUris(
                uriLogout = "sample://uri.logout",
                uriChat = "sample://uri.chat",
                uriDashboard = "sample//uri.dashboard",
                uriHelp = "sample://uri.help",
                uriKyc = "sample://uri.kyc",
                uriUpdateApp = "sample://uri.update.app"
            ),
            httpClientConfig = HttpClientConfig(),
            logger = InternalLogger(),
            tokenKeyMasterUri =  URI("android-keystore://stone-mobile")
        )
```

- `application`: Trata-se da instância do Application do seu app.

- `environment`: Existem 3 ambientes para os quais a sdk pode apontar: `Homolog`, `Sandbox` e `Production` para fins de teste use o `Environment.Sandbox`.

- `appInfo`: Informações referentes ao app como nome, versão e buildId.

- `client_id`: Identificador fornecido pelo time de suporte OpenBank.

- `authFlowUIConfig`: Com esta configuração é possível passar o tema da sua aplicação para a SDK, assim as cores principais do estilo do seu app serão aplicadas nas telas internas da SDK.

- `httpClientConfig`: Trata-se de configurações HTTP customizadas do cliente, como `interceptors`, `connectionTimeoutMs`, `readTimeoutMs`, `writeTimeoutMs` e `networkInterceptors`.

- `tokenKeyMasterUri`: Uma URI para a chave mestra no formato `android-keystore://`. Essa chave será utilizada para acessar o Keystore do android e salvar o token do usuário de forma segura.

- `deepLinkUris`: Uris usadas para fazer a navegação para Activities externas a sdk. Exemplo, a `uriLogout` se refere a Activity que o usuário deve ser redirecionada depois que ele for deslogada do app, essa navegação é feita por deeplink.

<br>

##### **Iniciando fluxo de Autenticação e verificação de KYC**
---

Para iniciar o fluxo de autenticação e verificação de KYC é necessário chamar o método abaixo.

```python
contaStoneSdk.startAuthAndVerificationFlowForResult(
            context = this,
            params = VerificationParams(
                launchMode = VerificationLaunchMode.StartingApp,
                authMode = AuthFlowMode.RegisteredUser
            ),
            requestCode = LOGIN_RC
        )
```

O atributo `params` recebe dois argumentos: O modo de inicialização, o qual define como que o fluxo deve ser iniciado e o `authMode` que neste caso sempre vai ser `AuthFlowMode.RegisteredUser`. O modo de inicialização pode ser:

- `StartingApp` - Inicia todo o fluxo de autenticação e check de KYC.

- `AccountSelectionRequest` - Exibe a tela de troca de conta e lida com a escolha do usuário nos casos em que o usuário em questão possui mais de uma conta de pagamento.

- `PushNotificationReceived` - Deve ser iniciado ao receber um push notification referente ao processo de abertura de conta.

- `NewAccountCreated` - Deve ser chamado após a criação de uma nova conta de pagamento para que seja verificado se esta conta não possui nenhuma pendência em seu cadastro.

Este método inicia a Activity principal da SDK e executa os fluxos internos de autenticação e verificação de KYC. Quando o processo é finalizado a Conta Stone SDK retorna um `Result` através do `onActivityResult` da Activity que deve ser tratado pelo app.

<br>

##### **Lidando com o resultado da SDK**
---

Ao finalizar o fluxo de autenticação e verificação a SDK emite um resultado para o app informando o desfecho do fluxo. Segue abaixo um exemplo de como tratar o resultado emitido pela Conta Stone SDK e o que cada um significa.

```python
 override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
         super.onActivityResult(requestCode, resultCode, data)
         if (requestCode == LOGIN_RC) {
             val result = contaStoneSdk.parseAuthAndVerificationResult(data)
 
             when (result) {
                 is AuthAndVerificationResult.Ok -> toast("User is authenticated")
                 is AuthAndVerificationResult.MissingData -> toast("some information is missing")
                 is AuthAndVerificationResult.UserCancelled -> toast("User cancelled flow")
                 is AuthAndVerificationResult.Error -> toast("Error during login ${result.error}")
                 is AuthAndVerificationResult.UserLoggedOut -> toast("User requests logout")
                 is AuthAndVerificationResult.BlockedUser -> toast("User is blocked")
             }
         }
     }
    }
```
<br>

##### **Como fazer logout**
---

Para deslogar o usuário podemos fazer uma chamada para o método de logout seguindo o exemplo abaixo.

```python
contaStoneSdk.logout {
            if (it != null) {
                toast("Error on logout. Try again!")
            } else toast("user successfully logged out")
        }
```

Quando a exception é nula o logout ocorreu com sucesso, quando não, algum erro ocorreu durante o fluxo.

<br>

##### **Obtendo o Client autenticado**
---

A authSDK é responsável por todo o processo de autenticação incluindo a adição do token no header das chamadas para a API do Stone Openbank. Para isso a SDK fornece um `OkHttpClient` configurado que pode ser utilizado nas chamadas HTTP do seu app. Este client possui [certificate pinning](https://owasp.org/www-community/controls/Certificate_and_Public_Key_Pinning) com os certificados da API do Stone OpenBank e é possível acessá-lo chamando o método `contaStone.auth().client()`.

```python
private fun performAuthenticatedRequest() {
        val httpService = HttpService.BankingGatewaySandbox
        val client = contaStoneSdk.auth().getOkHttpClient(httpService)

        val request = Request.Builder()
            .url("${httpService.url}/api/v1/institutions")
            .get()
            .build()

        val callback = object : Callback {
            override fun onFailure(call: Call, e: IOException) {
                runOnMainThread {
                    toast("Error fetching institutions $e")
                }
            }

            override fun onResponse(call: Call, response: Response) {
                runOnMainThread {
                    toast("Request executed successfully")
                }
            }
        }

        client.newCall(request).enqueue(callback)
    }
```

<br>

<!---
##### **Como inicializar o Aprovador**
---

Para conseguir iniciar o aprovador é necessário fazer a chamada conforme o exemplo abaixo:

```python
contaStoneSdk.startApproverForResult(
                        source = this,
                        requestCode = APPROVER_RQ,
                        params = ApproverParams(loggedAccount, ApproverLaunchMode.SDKLaunchMode)
                    )
```

Para recuperar o `loggedAccount` a Conta Stone SDK disponibiliza a sessão do usuário logado com todas as informações que o `LoggedAccount` precisa:

```python
contaStoneSdk.getSession(
                onComplete = { result ->
                    when (result) {
                        is SessionResult.Success -> {
                                currentAccount?.paymentAccount?.let {
                                        LoggedAccountInfo(
                                            id = it.id,
                                            accountNumber = it.accountCode,
                                            accountOwner = currentAccount?.owner?.name.orEmpty(),
                                            accountOwnerDocument = currentAccount?.owner?.document.orEmpty(),
                                            bankName = "Stone Pagamentos S.A",
                                            bankNumber = "197",
                                            branchNumber = "0001",
                                            userLoggedName = profile.fullName
                                        )
                                    }
                                }
                        is SessionResult.HasNoActiveSession -> redirectToLogin()
                    }
                },
                onError = {
                    toast("Error trying to get session")
                }
            )
```)
--->

<br>

## Integração iOS
---
<br>

##### **Contato**
---

Se durante a integração encontrar algum problema ou ponto de melhoria entre em contato com a gente através da ferramenta de suporte.


##### **Instalação**
---

###### **Requisitos**

- iOS 10.0
- Xcode 11.7

<br>

###### **Configuração**

Antes de começar a usar o ContaStoneSDK é necessário seguir alguns procedimentos:


1. [Baixe o arquivo zip](https://github.com/stone-co/conta-stone-sdk-sample-ios/releases/tag/0.2.0) no link com os frameworks necessários.
2. Extraia a pasta Frameworks no diretório raiz do projeto.
3. No target do projeto acesse a guia `General` e em `Frameworks, Libraries, and Embedded Content` adicione os frameworks:

	- ContaStoneSDK.framework
	- CryptoSwift.framework
	- JOSESwift.framework
	- TinyConstraints.framework
	- XCoordinator.framework
	
	<br>

4. Na guia `Build Settings`, em `Build Options`, selecione `NO` para a configuração `Enable Bitcode`.
5. Na guia `Build Settings`, em `Runpath Search Paths`, adicione a entrada `@executable_path/Frameworks/ContaStoneSDK.framework/Frameworks/`.
6. Logo abaixo em `Framework Search Paths`, adicione a entrada `$(PROJECT_DIR)/Frameworks/ContaStoneSDK.framework/Frameworks/` no modo recursivo.
7. Em `Build Phases` adicione um novo script chamado "Sign" (Em Build Phases, clique sinal de "mais" e selecione New Run Script Phase).

```python
pushd ${TARGET_BUILD_DIR}/${PRODUCT_NAME}.app/Frameworks/ContaStoneSDK.framework/Frameworks

for EACH in *.framework; do
	echo "-- signing ${EACH}"
	/usr/bin/codesign --force --deep --sign "${EXPANDED_CODE_SIGN_IDENTITY}" --entitlements "${TARGET_TEMP_DIR}/${PRODUCT_NAME}.app.xcent" --timestamp=none
	$EACH
done

popd
```

8. Adicione dependências:

```python
// Cocoapods

pod 'Alamofire', '4.8.2'
pod 'RxSwift', '~> 5'
pod 'RxCocoa', '~> 5'
pod 'lottie-ios', '3.1.6'
pod 'AloeStackView', '1.2.0'

// Carthage

github "Alamofire/Alamofire" "4.8.2"
github "ReactiveX/RxSwift" "5.1.1"
github "airbnb/lottie-ios" "3.1.6"
github "airbnb/AloeStackView" "v1.2.0"
```



##### **USO**
---

###### **Configurando o AppDelegate**

```python
import UIKit
import ContaStoneSDK

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
		ContaStone.configure(
			id: "john.doe@openbank.com",
			scopes: ["offline_access"],
			environmentType: .sandbox, // .homol, .sandbox, .production
			delegate: self
		)

		return true
	}
}

extension AppDelegate: ContaStoneDelegate {
	func refreshApp() {}
	func sessionRevoked() {}
	func loggedOut() {}
	func showHelpCenter() {}
	func showChat() {}
	func showFrequentlyAskedQuestions() {}
}
```

###### **Autenticação**

```python
import UIKit
import ContaStoneSDK

class ViewController: UIViewController {
	func checkAuthenticationState() {
		if ContaStone.isAuthenticated {
			ContaStone.currentAcount.name // John Doe Inc
		} else {
			ContaStone.login(checkKYC: true) { /* callback */ }
		}
	}
}
```

###### **Logout**

```python
import UIKit
import ContaStoneSDK

class ViewController: UIViewController {
	func logout() {
		ContaStone.logout { /* callback */ }
	}
}
```
<!---
##### **Aprovador**

```python
	var approverCoordinator: ApproverCoordinator?

	func showApprover() {
        let coordiantor = ApproverCoordinator() { _ in
            self.approverCoordinator = nil
        }
        present(coordiantor.rootViewController, animated: true, completion: nil)

        approverCoordinator = coordiantor // Holds the instance
	}
```
--->

###### **Requisições**

```python
class ViewController: UIViewController {
	func fetchBalance() {
	   let id = ContaStone.currentAcount.id
	   let endpoint = Endpoint<BalanceResponse>(method: .get, path: "/api/v1/accounts/\(id)/balance")

	   ContaStone.performRequest(endpoint) { result in
			switch result {
			case .success(let response):
				/* callback */

			case .failure(let error):
				/* callback */
		   }
	   }
	}
}
```

<br>

##### **Exemplo**
---

Antes de abrir o projeto de exemplo, é necessário executar o script de bootstrap.

```
./bootstrap
open Sample.xcworkspace
```