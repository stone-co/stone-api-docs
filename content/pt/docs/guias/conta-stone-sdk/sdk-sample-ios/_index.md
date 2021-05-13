---
title: "Sample iOS"
linkTitle: "Sample iOS"
date: 2021-03-20T10:00:00-03:00
lastmod: 2021-03-23T11:00:00-03:00
weight: 2
draft: true
---

---

SDK de integração para iOS.

#### **Contato**
---

Se durante a integração encontrar algum problema ou ponto de melhoria entre em contato com a gente através do Azendoo.


#### **Instalação**
---

##### **Requisitos**

- iOS 10.0
- Xcode 11.7

<br>

##### **Configuração**

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



#### **USO**
---

##### **Configurando o AppDelegate**

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

##### **Autenticação**

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

##### **Logout**

```python
import UIKit
import ContaStoneSDK

class ViewController: UIViewController {
	func logout() {
		ContaStone.logout { /* callback */ }
	}
}
```

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

##### **Requisições**

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

#### **Exemplo**
---

Antes de abrir o projeto de exemplo, é necessário executar o script de bootstrap.

```
./bootstrap
open Sample.xcworkspace
```
