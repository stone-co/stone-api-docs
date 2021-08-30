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
<br>Assim, de maneira segura, os usuários poderão realizar os processos de autenticação e KYC interagindo de maneira direta com a Stone, mas por meio da SDK integrada pelo parceiro. 

A Conta Stone SDK funciona como ponto de entrada para os três processos abaixo:
- SDK de Autenticação (Auth SDK): responsável por executar o processo de Autenticação seguindo os padrões especificados.
- Verificação de KYC (Pegasus SDK):  responsável por capturar as informações do usuário que está realizando cadastro na conta.

[//]: <> (Aprovação (Approver SDK): Responsável por realizar aprovações ou reprovações de transações)

Após obter o seu [Token de Acesso]({{< relref "/docs/guias/token-de-acesso">}}), caso deseje usar nossa SDK e disponibilizar as etapas acima descritas aos seus usuários, siga os próximos passos para instalação do kit para [iOS]({{< relref "/docs/guias/sdk/#integração-ios">}}) e [Android]({{< relref "/docs/guias/sdk/#integração-android" >}}).

<br>

## Integração Android
---
<br>

A Conta Stone SDK é responsável por todo o fluxo de login e Know Your Customer da [Stone Openbank API](/docs/guias/stone-open-banking/overview/).


##### **Contato**
---

Se durante a integração você encontrar algum problema ou ponto de melhoria, entre em contato com a gente através da ferramenta de suporte.



##### **Como funciona**
---

A Conta Stone SDK é o ponto de entrada para acesso às nossas SDKs de autenticação, aprovação e verificação de [KYC](https://en.wikipedia.org/wiki/Know_your_customer) (*Know Your Customer*).

 - A SDK de autenticação é responsável por executar todo o processo de autenticação seguindo as diretrizes do [OAuth2](https://oauth.net/2/).

 - A SDK de aprovação é responsável pelo processo de aprovação e rejeição de transações.

 - A SDK de KYC é responsável por capturar as informações do usuário que está realizando cadastro na conta.

<br>

##### **Como Integrar com a Conta Stone SDk**
---

Antes de começar a integração é necessário obter uma chave de acesso ao repositório, pois trata-se de um repositório privado. Para obter essa chave, entre em contato com a gente.

No arquivo `build.gradle` do projeto, adicione a URL do repositório e substitua o `{access-key}` pela chave fornecida.

```kotlin
maven { url "https://packagecloud.io/priv/${access-key}/Stone/stoneid/maven2"}
```

Também é preciso adicionar o Jetpack, pois usamos algumas libs que estão disponíveis nesse repositório.

```kotlin
maven { url 'https://jitpack.io' }
```

Importe a dependência da Conta Stone SDK.

```kotlin
implementation 'co.stone:stone-android:${latest_version}'
```

A Conta Stone SDK utiliza o Firebase para implementar alguns de seus serviços, logo é necessário ter um projeto no Firebase e integrá-lo no seu app. Para mais informações sobre como adicionar o Firebase ao seu projeto, acesse este [link](https://firebase.google.com/docs/android/setup).

Sincronize o projeto e pronto, já é possível utilizar a Conta Stone SDK!

<br>

##### **Inicializando a SDK**
---

Uma vez que a dependência foi importada, o passo seguinte da integração é inicializar a SDK no seu `Application`. Para isso é necessário especificar os parâmetros abaixo.

```kotlin
class App : Application() {

	private val environment = Environment.SANDBOX

	val stoneSdk by lazy {
        Stone.init(
            this,
            environment,
            AppInfo(
                name = "YOUR_APP_NAME",
                version = BuildConfig.VERSION_NAME,
                buildId = "NA",
                applicationId = BuildConfig.APPLICATION_ID,
                themeId = R.style.YOUR_APP_THEME
            ),
            AuthInfo(
                clientId = "YOUR_CLIENT_ID",
                tokenMasterKeyUri = URI("android-keystore://cssdk-sample-token-key"),
                httpClientConfig = HttpClientConfig()
            ),
            DeepLinkUris(
                uriLogout = "sample://uri.logout",
                uriChat = "sample://uri.chat",
                uriHelp = "sample://uri.help",
                uriKyc = "sample://uri.kyc",
                uriUpdateApp = "sample://uri.forceupdate",
                uriDashboard = "sample://uri.dashboard"
            )
        )
    }

    override fun attachBaseContext(base: Context) {
        super.attachBaseContext(base)
        StoneContext.setContext(base)
    }
}
```

- `application`: Trata-se da instância do `Application` do seu app;

- `environment`: Existem 3 ambientes para os quais a SDK pode apontar: `HOMOLOGUE`, `SANDBOX` e `PRODUCTION`. Para fins de teste, use o `Environment.SANDBOX`;

- `appInfo`: Informações referentes ao app como nome, versão e buildId;

- `authInfo`: Informações referentes a autenticação como clientId (fornecido pelo time de suporte OpenBank), configuração do `OkHttp` e URI para a chave mestra no formato `android-keystore://` (será utilizada para acessar o Keystore do Android e salvar o token do usuário de forma segura);

- `deepLinkUris`: URIs usadas para fazer a navegação para Activities externas à SDK. Exemplo: a `uriLogout` se refere à Activity para a qual o usuário deve ser redirecionado depois que ele for deslogado do app. Essa navegação é feita por deeplink;

- `StoneContext.setContext()`: Precisamos ter acesso ao `Context` da aplicação para realizar algumas operações internas relacionadas ao ciclo de vida do app.

<br>

##### **Iniciando fluxo de Autenticação e verificação de KYC**
---

Para iniciar o fluxo de autenticação e verificação de KYC, é necessário chamar o método abaixo.

```kotlin
stoneSdk.session
	.verify(activity = this, params = SessionVerificationParams(Full))
	.runAsync(
		onSuccess = { result -> /* HANDLE RESULT */ },
		onFailure = { error -> /* HANDLE ERROR */ }
	)
```

Esse método inicia a Activity principal da SDK e executa os fluxos internos de autenticação e verificação de KYC. Quando o processo é finalizado, a Conta Stone SDK retorna um `FlowResult` que deve ser tratado pelo app.

<br>

##### **Lidando com o resultado da SDK**
---

Ao finalizar o fluxo de autenticação e verificação, a SDK emite um resultado para o app informando o desfecho do fluxo. Segue abaixo um exemplo de como tratar o resultado emitido pela Conta Stone SDK e o que cada um significa.

```kotlin
when (result) {
	is FlowResult.Completed -> handleSuccess()
	is FlowResult.Cancelled -> handleCancellation()
	is FlowResult.Failed -> handleError()
}
```
<br>

##### **Como fazer logout**
---

Para deslogar o usuário, podemos fazer uma chamada para o método de logout seguindo o exemplo abaixo.

```kotlin
stoneSdk.auth
	.logout()
	.runAsync(
		onSuccess = { /* HANDLE SUCCESS */ },
		onFailure = { error -> /* HANDLE ERROR */ }
	)
```

<br>

##### **Obtendo o Client autenticado**
---

A authSDK é responsável por todo o processo de autenticação, incluindo a adição do token no header das chamadas para a API do Stone Openbank. Para isso a SDK fornece um `OkHttpClient` configurado que pode ser utilizado nas chamadas HTTP do seu app. Esse client possui [certificate pinning](https://owasp.org/www-community/controls/Certificate_and_Public_Key_Pinning) com os certificados da API do Stone OpenBank e é possível acessá-lo chamando o método `stoneSdk.auth.getOkHttpClient()`.

```kotlin
private suspend fun getInstitutions(): List<Institution> {
	val httpService = HttpService.BankingGatewaySandbox

	val client = stoneSdk.auth.getOkHttpClient().run()

	val request = Request.Builder()
		.url("${httpService.url}/api/v1/institutions")
		.get()
		.build()

	val response = client.newCall(request).execute()

	return InstitutionMapper.toDomain(response)
}
```

<br>

<!---
##### **Como inicializar o Aprovador**
---
Para iniciar o aprovador é necessário fazer a chamada conforme o exemplo abaixo:

```kotlin
stoneSdk.approver
	.manageApprovals(activity = this, params = ManageApprovalsParams(approverAccountInfo))
	.runAsync(
		onSuccess = { result -> /* HANDLE RESULT */ },
		onFailure = { error -> /* HANDLE ERROR */ }
	)
```

Para recuperar o `approverAccountInfo` a Conta Stone SDK disponibiliza a sessão do usuário logado com todas as informações que o `ApproverAccountInfo` precisa:

```kotlin
stoneSdk.session
	.getSession()
	.runAsync(
		onSuccess = { session -> 
			val currentaccount = session.currentAccountOrThrow

			val approverAccountInfo = ApproverAccountInfo(
                userId = session.user.id,
                userName = session.user.name,
                accountOwner = currentaccount.owner.name,
                accountOwnerDocument = currentaccount.owner.document,
                accountNumber = currentaccount.payment.accountCode,
                bankName = StoneOpenBank.institutionName,
                bankNumber = StoneOpenBank.institutionCode,
                branchNumber = StoneOpenBank.agencyCode
            )
 		},
		onFailure = { error -> /* HANDLE ERROR */ }
	)
```
--->

##### **Integração com Coroutines e RxJava**
---

A API pública da Conta Stone SDK retorna sempre um `Runnable<T>`, com ele é possível escolher de qual forma deseja executar a operação:
- `runAsync()`: utiliza callbacks (útil se você estiver utilizando Java)
- `run()` e `runCatching()`: são `suspend fun`, devem ser chamadas dentro de um Coroutine Scope (recomendado para quem utiliza Kotlin)
- `asFlow()`: retorna um `Flow` do Coroutines
- `asSingle()`, `asObservable()`, `asCompletable()` e `asFlowable()`: integração com RxJava

Exemplo com Coroutines:
```kotlin
viewModelScope.launch {
	val session = stoneSdk.session.getSession().run()
}
```

Exemplo com RxJava:
```kotlin
stoneSdk.session
	.getSession()
	.asSingle()
	.subscribeBy(
		onSuccess = { session -> ... },
		onError = { error -> ... } 
	)
```

<br>

## Integração iOS
---
<br>

##### **Contato**
---

Se durante a integração encontrar algum problema ou ponto de melhoria, entre em contato com a gente através da ferramenta de suporte.

##### **Instalação**
---

###### **Requisitos**

- iOS 10.0
- Xcode 11.7

<br>

###### **Configuração**

Antes de começar a usar a Conta Stone SDK, é necessário seguir alguns procedimentos:


1. [Baixe o arquivo zip](https://github.com/stone-co/conta-stone-sdk-sample-ios/releases/tag/0.2.0) no link com os frameworks necessários.
2. Extraia a pasta Frameworks no diretório raiz do projeto.
3. No target do projeto, acesse a guia `General` e, em `Frameworks, Libraries, and Embedded Content`, adicione os frameworks:

	- ContaStoneSDK.framework
	- CryptoSwift.framework
	- JOSESwift.framework
	- TinyConstraints.framework
	- XCoordinator.framework
	
	<br>

4. Na guia `Build Settings`, em `Build Options`, selecione `NO` para a configuração `Enable Bitcode`.
5. Na guia `Build Settings`, em `Runpath Search Paths`, adicione a entrada `@executable_path/Frameworks/ContaStoneSDK.framework/Frameworks/`.
6. Logo abaixo em `Framework Search Paths`, adicione a entrada `$(PROJECT_DIR)/Frameworks/ContaStoneSDK.framework/Frameworks/` no modo recursivo.
7. Em `Build Phases` adicione um novo script chamado "Sign" (em Build Phases, clique sinal de "mais" e selecione New Run Script Phase).

```swift
pushd ${TARGET_BUILD_DIR}/${PRODUCT_NAME}.app/Frameworks/ContaStoneSDK.framework/Frameworks

for EACH in *.framework; do
	echo "-- signing ${EACH}"
	/usr/bin/codesign --force --deep --sign "${EXPANDED_CODE_SIGN_IDENTITY}" --entitlements "${TARGET_TEMP_DIR}/${PRODUCT_NAME}.app.xcent" --timestamp=none
	$EACH
done

popd
```

8. Adicione dependências:

```swift
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

```swift
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

```swift
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

```swift
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

```swift
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

```swift
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
