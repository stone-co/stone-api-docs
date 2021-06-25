---
title: "Autenticação"
slug: "autenticacao-guides"
hidden: false
date: "2019-05-28T18:04:38.641Z"
lastmod: "2020-07-20T07:37:56.473Z"
weight: 3
---

Detalhes sobre o processo de se autenticar na nossa API.

---

<br>

Segurança sempre foi um assunto complexo, principalmente por ter uma terminologia específica. Para facilitar ao máximo a integração com a nossa API, procuramos adotar padrões estabelecidos de mercado.



#### **Autenticação de Aplicativos Parceiros**


Cada Aplicativo recebe um identificador exclusivo chamado [clientID](/docs/guias/integracao/cadastro-da-aplicacao/#credenciais-da-minha-aplicação) quando é criado. Esse ID não pode ser modificado e será usado no token de acesso do seu aplicativo quando chamar a API.

Outra informação importante é o [par de chaves](/docs/guias/integracao/cadastro-da-aplicacao/gerando-o-par-de-chaves/) do seu aplicativo, que deve ser mantida confidencial em todos os momentos. Se alguém obtiver acesso a sua chave privada, essa pessoa poderá acessar recursos protegidos em nome do seu aplicativo. Isso não pode acontecer sob hipótese alguma. 

O desenvolvedor deve usar essa chave privada para assinar os tokens enviados para a Stone e nos enviar a chave pública para verificarmos a assinatura.



#### **Autenticação com o Auth e Open ID Connect**


[OAuth 2.0](https://oauth.net/2/) é um padrão de autorização que permite ao usuário conceder acesso limitado a seus recursos na Conta Stone para Aplicativos de Parceiros, sem precisar expor suas credenciais. Ou seja, o cliente não precisa compartilhar seu login e senha com ninguém. 

Já o [OpenID Connect](https://openid.net/connect/) é uma camada de identidade construída em cima do [OAuth 2.0](https://oauth.net/2/) e que permite a fácil verificação da identidade do usuário, bem como a capacidade de obter informações básicas de perfil do provedor de identidade (no caso, a Conta Stone).




#### **Autenticando a Aplicação Parceira**


A nossa API só aceita chamadas autenticadas, ou seja, chamadas cujo sujeito da ação conseguimos identificar.

Para isso exigimos que nas [requisições HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) exista no cabeçalho um campo chamado `authorization`, cujo valor será "Bearer" seguido do token de acesso. Os próximos tópicos explicam como obter esse token de acesso.

Exemplo de cabeçalho de uma chamada autenticada:

```
GET /api/v1/accounts HTTP/1.1
Host: sandbox-api.openbank.stone.com.br
User-Agent: curl/7.61.1
Accept: */*
authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
<br>

Dessa forma, após o cadastro da Aplicação do desenvolvedor, é necessário implementar a autenticação.

Como foi detalhado acima, nosso fluxo se baseia na especificação [OAuth 2.0](https://oauth.net/2/) e [OpenID Connect](https://openid.net/connect/). O fluxo de integração [OAuth 2.0](https://oauth.net/2/) que usamos é o de _client credentials_. Neste fluxo, o desenvolvedor irá precisar:

**1. Gerar um token [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token) com as configurações da sua Aplicação, assinando com sua chave privada.**

**2. Fazer uma requisição `POST` para nosso servidor de autenticação, enviando o JWT. Se for um token válido, enviaremos como resposta um token de acesso.**

**3. Usar esse `access_token` para fazer as chamadas autenticadas.**

<br>

#### **1. Gerando o token JWT**

[JWT](https://en.wikipedia.org/wiki/JSON_Web_Token) é uma especificação para gerarmos _tokens_ que sejam assinados e/ou criptografados. [Nesta página](https://jwt.io/) temos várias bibliotecas de desenvolvimento em várias linguagens que implementam esta especificação.

Basicamente, um JWT possui 3 partes:

- **header**: possui informações sobre o algoritmo de criptografia utilizado, entre outros metadados deste processo, como um id da chave utilizada. Na nossa API utilizaremos sempre o algoritmo "RS256". Falaremos mais sobre ele. Um exemplo de *header* seria:


```json
{
  "alg": "RS256",
  "typ": "JWT"
}
```


Este deve ser encondado na *base 64* para ser incluído no token. Para o exemplo, fica: `eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9`.
- **payload**: um conjunto de alegações (_claims_, do inglês) que possuem a estrutura chave/valor. É aqui que colocamos informações como tempo de expiração do token, qual o id da Aplicação e etc.
- **signature**: a assinatura do header e payload usando o algoritmo descrito no header e a chave privada. 


#### **Claims**

Para conseguir se autenticar com sucesso, o desenvolvedor precisará colocar nos _claims_ os seguintes valores:

<br>

| Nome     | Valor                                                                                                                                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| exp      | Tempo de expiração do token em segundos desde o início da era UNIX (1970). É UTC e não pode ser maior que 15 min. Ex: "exp": 1542235633                                                                                                                                   |
| nbf      | "Not before", ou seja, data a partir da qual o token é válido. É UTC. Ex: "nbf": 1542235633                                                                                                                                                                               |
| aud      | Quem é a "audiência" deste token. No caso, é o nosso servidor de autenticação. Para o ambiente de Sandbox será: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank . Para Produção será: https://accounts.openbank.stone.com.br/auth/realms/stone_bank |
| realm    | Qual é o "reino" das nossos usuários. Será sempre "stone_bank".                                                                                                                                                                                                           |
| sub      | O sujeito referente ao token. Deve ser o ClientID enviado ao desenvolvedor pós-cadastro da Aplicação.                                                                                                                                                                     |
| clientId | Mesmo valor de sub, ou seja, o ClientID enviado ao desenvolvedor pós-cadastro da Aplicação.                                                                                                                                                                               |
| jti      | Identificador único do token gerado. Normalmente se utiliza um UUID, mas não é obrigatório usar esse formato desde que a unicidade seja garantida. [Mais informações](https://tools.ietf.org/html/rfc7519#section-4.1.7)                                                                                                      |
| iat      | Momento em que o token foi gerado. É UTC. Ex. "iat": 1542235633                                                                                                                                                                                                           |



Usando a **chave privada** e o algoritmo "RS256", o desenvolvedor consegue gerar e assinar o Token [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token) com qualquer uma das libs listadas [neste site](https://jwt.io/).

Nós temos guardada de forma segura a **chave pública** que usaremos para validar este token.
 
Esse é um processo de **criptografia assimétrica**, no qual usaremos o par de chaves pública e privada gerado pela desenvolvedora no momento do cadastro da Aplicação. 


#### **RS256**

Este algoritmo especificado [nesta RFC](https://tools.ietf.org/html/rfc7518#section-3.3) usa criptografia "RSASSA-PKCS1-v1_5 com SHA-256". É o mesmo padrão de integração das APIs que muitas outras grandes empresas utilizam. 

<br>


#### **2. Fazendo a requisição para receber o token de acesso**


Após a geração do token local, é preciso fazer uma chamada para o nosso servidor de autenticação para que a gente faça a validação e retorne um `access_token` nosso.

Esta chamada será nas seguintes URLs (por ambiente):

- _Sandbox_: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token
- _Produção_: https://accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token

A chamada é com o método `POST` com o header  `Content-Type`  e `User-Agent`.  O `Content-Type` informado deve ser `x-www-form-urlencoded` (o mesmo usado por submissão de formulários HTML) e o header `User-Agent` deve estar habilitado.


Ex.:

```json
{
  "user-agent": "Nome da aplicação",
  "content-type": "application/x-www-form-urlencoded"
}
```

##### **Glossário**

| Nome                  | Valor                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| client_id             | É o valor enviado para o desenvolvedor pós-cadastro da Aplicação.                                                                    |
| grant_type            | Será sempre "client_credentials".                                                                                                    |
| client_assertion      | Aqui deve ser o token que o desenvolvedor gerou.                                                                                     |
| client_assertion_type | Sempre será urn:ietf:params:oauth:client-assertion-type:jwt-bearer, que é o que fecha o fluxo de client credentials para o servidor. |


##### **Examples**


{{< alert title="Curl" >}}
    
```json
{
  curl -X POST https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token -H 'content-type: application/x-www-form-urlencoded' -d 'client_id=ID_EXEMPLO&grant_type=client_credentials&client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer&client_assertion=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c'
}
```
{{< /alert >}}

{{< alert title="Python" >}}
    
```python
import jwt
import time
import requests
import subprocess

class AppData:
  def __init__(self, client_id, base_url, base_auth_url, private_key):
    self.client_id = client_id
    self.base_url = base_url
    self.base_auth_url = base_auth_url
    self.private_key = private_key


def getApplicationData():
    return AppData(
        'insira aqui seu client_id',
        'https://sandbox-api.openbank.stone.com.br/api/v1',
        'https://sandbox-accounts.openbank.stone.com.br',
        private_key
    )

private_key = """-----BEGIN RSA PRIVATE KEY-----

                Insira aqui sua private_key

-----END RSA PRIVATE KEY-----"""


def getToken():

    app_data = getApplicationData()

    base_url = f'{app_data.base_auth_url}/auth/realms/stone_bank'
    auth_url = f'{base_url}/protocol/openid-connect/token'

    payload = {
        'exp': int(time.time()) + 3600,
        'nbf': int(time.time()),
        'aud': base_url,
        'realm': 'stone_bank',
        'sub': app_data.client_id,
        'clientId': app_data.client_id,
        'jti': str(time.time()),
        'iat': int(time.time())
    }

    token = jwt.encode(payload, app_data.private_key, algorithm='RS256')

    headers = {
        'Content-Type': 'application/x-www-form-urlencoded',
        'User-Agent': 'Insira aqui o Nome da Aplicação'
    }

    token_payload = {
        'client_id': app_data.client_id,
        'grant_type': 'client_credentials',
        'client_assertion': token.decode(),
        'client_assertion_type': 'urn:ietf:params:oauth:client-assertion-type:jwt-bearer'
    }

    return requests.post(auth_url, data=token_payload, headers=headers)


# COMENTAR PRA NÃO COPIAR O TOKEN
response = getToken()
access_token = response.json()['access_token']

print (access_token)
```
{{< /alert >}}


##### **Response**


```json
{
    "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ijh3eWRUZGpzTEdYVSJ9.eyJqdGkiOiIzM2RlNjg2Mi1iYmVkLTQ3ZWYtYTY5Yi0wNDAzNTI0YTRhNGEiLCJleHAiOjE1NTkyNDg3OTUsIm5iZiI6MCwiaWF0IjoxNTU5MjQ3ODk1LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJjMWExZmE5NC0zOTc4LTRhNjgtODBlNy1mZWU2ZTkwNmNiMmUiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJhZG1pbi1jbGkiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiJhN2YxN2QxMC1jMGY1LTQzMzItOWE5MC1lNDQxMTVmMWNlMGEiLCJhY3IiOiIxIiwic2NvcGUiOiJleHBlbmQ6dHJhbnNmZXJzOmludGVybmFsIGVudGl0eTpsZWdhbF93cml0ZSBlbnRpdHk6d3JpdGUgcHJpbmNpcGFsOmNvbnNlbnQgZW1haWwgZXhwZW5kOnRyYW5zZmVyczpleHRlcm5hbCBzdG9uZV9zdWJqZWN0X2lkIGV4cGVuZDpyZWFkIGV4cGVuZDpib2xldG9pc3N1YW5jZSBlbnRpdHk6cmVhZCBwcm9maWxlIHBheW1lbnRhY2NvdW50OiogZXhwZW5kOnBheW1lbnRzIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsInN0b25lX3N1YmplY3RfaWQiOiJ1c2VyOjNmMDcwN2NiLWEyYzgtNDlhMS04NDc4LWFjMDg1MGY5Njc4MCIsIm5hbWUiOiJKb2FvIiwicHJlZmVycmVkX3VzZXJuYW1lIjoiam9hby5leGVtcGxvQGVtYWlsLmNvbS5iciIsImdpdmVuX25hbWUiOiJKb2FvIiwiZW1haWwiOiJqb2FvLmV4ZW1wbG9AZW1haWwuY29tLmJyIn0.baf0-ZMg_IPtoReTpQBnMIYPjrLWFklPT7T1CGE2ecxfxt-a3h1CSdveK0Xd0f9FWna6obcSIonHn7HD0mJnxwBoIK8w6_cg_ODTS-l2jgGWVTl-jN41rdyTg5kgtTT6M3v02QJxTOfklo9mpW4tX8cZorx5vP_ykb5Kk186PGxYTJ9mGwQEuyrHl7-mc8aN7x10Ue7P_fk2Br43T2uR7LoFFIVM9I45p1hntZx-e59alleIuUqnZzk5Vo8knk67ZEJEAWOiigS0yyyy9gT3wqPypBYnoP3SMVws7e6lfKuZasCS58z8arJiYVQVgF6xSoQQdDBTY4I1_5kL-phmAA",
}
```

<br>


#### **3. Usando o access_token da resposta**


Se tudo deu certo no passo anterior, a resposta do servidor será um JSON com uma chave `access_token`, onde terá o valor de um token de sessão.

Como falamos no início dos tópicos anteriores, **para usar este token basta colocá-lo no header `Authorization` com o valor `Bearer ACCESS_TOKEN`**. Aqui, o desenvolvedor deve substituir "ACCESS_TOKEN" pelo valor recebido.



{{% pageinfo %}}
**Autenticação nos exemplos**

Cada exemplo de endpoint desta documentação tem um campo especial para o ACCESS_TOKEN.

{{% /pageinfo %}}


Pronto! Com isto já é possível fazer uma chamada autenticada para a nossa API. A URL é (por ambiente):

- _Sandbox_: https://sandbox-api.openbank.stone.com.br
- _Produção_: https://api.openbank.stone.com.br

<br>

**Bem-vindo ao time de fintechs do futuro!**

Esta chamada retorna um `access_token` que pode ser usado nas próximas chamadas.
