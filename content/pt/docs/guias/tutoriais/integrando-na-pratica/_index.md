---
title: "Integrando na Prática"
slug: "integrando-na-prática-guides"
hidden: false
createdAt: "2019-07-29T17:44:31.512Z"
updatedAt: "2020-12-29T13:59:12.916Z"
---

---

<br>

Neste tutorial vamos ver como:

- Gerar o token de [autenticação](https://docs.openbank.stone.com.br/docs/autenticacao-guides);
- Gerar o token e link de [consentimento](https://docs.openbank.stone.com.br/docs/consentimento-guides);
- Operar em contas que já concederam acesso à aplicação parceira.

Utilizaremos a linguagem Python na versão 3.7 para montar o token e a [biblioteca PyJWT](https://pyjwt.readthedocs.io/en/latest/) para assiná-lo.


{{% pageinfo %}}
**Conheça suas ferramentas**

É importante ler a documentação das bibliotecas utilizadas. A biblioteca utilizada neste tutorial, PyJWT, tem uma dependência extra para alguns algoritmos específicos. É o caso do algoritmo que será utilizado, RS256, que tem dependência da biblioteca `cryptography`. Por conta disso, esta biblioteca também precisa ser instalada.

{{% /pageinfo %}}

<br>

#### **1. Conhecendo os dados**


Como resultado do [cadastro da sua aplicação](https://docs.openbank.stone.com.br/docs/cadastro-da-aplicacao-guides), você recebeu um ClientID. Além disso, nos forneceu uma chave pública e manteve em segredo uma chave privada. Agora vamos ver como utilizá-los na prática.

Para montar os tokens, tenha em mãos o seu `redirect_uri` cadastrado, o seu ClientID e sua chave privada.

<br>

#### **2. Se preparando para gerar tokens**

Aqui vamos importar as bibliotecas que vamos utilizar e definir algumas constantes.

```JSON
import jwt
import time
import requests

MINUTE = 60
HOUR = 3600

CLIENT_ID = "92b5f9aa-9552-45f4-86cb-c0331c9178a2"
REDIRECT_URI = "https://myapplication.com/consent_callback"

ACCOUNTS_URL = "https://sandbox-accounts.openbank.stone.com.br"
API_URL = "https://sandbox-api.openbank.stone.com.br/api/v1"
```

Armazenamos a chave privada no arquivo `private.pem` e preparamos uma função para gerar o token. Essa função recebe um parâmetro com os claims e usa a chave privada para gerar e assinar o token.

Lembrando que se trata de um processo de criptografia assimétrica. Neste processo, o desenvolvedor assina o token com sua chave privada e a Stone utiliza a chave pública compartilhada com a gente para verificar que realmente foi a aplicação parceira quem gerou o token.


```JSON
def generate_token(claims):
    with open("private.pem", "r") as key_file:
        token = jwt.encode(claims, key_file.read(), algorithm='RS256')
        return token.decode()
```


Agora podemos assinar qualquer conjunto de claims e o resultado será um JWT. 

É possível utilizar claims arbitrários para testar essa funcionalidade:


```JSON
>>> generate_token({"claim": "qualquer"})
'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJjbGFpbSI6InF1YWxxdWVyIn0.hUGnpB5pI38TbQy8XDjXMmFTLWvYjk98UaTELfkJmHU0EK9-ZOTzSSNKdqOB0puGHr2xMRXta6WZLQmkRqJCVHSA6zsIdW0ABJiPaHXVOHFidq7iGZAbZtgHBf6b3ctko7OGxfLDJGedH3gYVh9i_tJ3S0kWpvLS7yMqNgwyHI4ZJecmL-qYD30FgrhGqyMK3LCxId7O_T6_QOisaLe_XXstXUnm82qvDh7iMZPqhV39V_CxnLl6CVZp2IfdQ3i8LAmtqaxhYSTODwBj47zOm_4bhfOcMO91LxY3wWW8fU7Qr8hyiUHqayBTiLRYqEGet_esQ_rrVFOn0F3tU0eWSA'
```


Se chegou a este mesmo resultado, você tem uma função que pode ser utilizada para assinar qualquer um dos seus tokens.

A biblioteca escolhida incluiu automaticamente no header as informações de tipo e algorítimo utilizados para gerar o token. Para se certificar da validade do token é possível utilizar o site [jwt.io](https://jwt.io).

Observe que trabalhamos com vários tokens JWT diferentes e utilizamos claims diferentes de acordo com a finalidade do token.

Para o token de autenticação, é preciso utilizar os claims descritos em [Autenticação](doc:autenticacao-guides); para o token de consentimento, serão utilizados os claims descritos em [Consentimento](doc:consentimento-guides).

<br>


#### **3. Montando o token de autenticação**


Inicialmente, é preciso consultar quais os claims específicos do token de autenticação na [documentação](https://docs.openbank.stone.com.br/docs/autenticacao-guides#section-claims).

Através da função que construimos é possível gerar e assinar esse token de forma simples.

Esse token será enviado para a Stone através de uma chamada para nosso servidor de autenticação, e enviaremos como resposta um `access_token`.

O `access_token` também é do tipo JWT, e funciona como uma chave de acesso para todas requisições na API.


```JSON
def auth_claims():
    now = int(time.time())
    return {
        "aud": f"{ACCOUNTS_URL}/auth/realms/stone_bank",
        "clientId": CLIENT_ID,
        "exp": now + 5 * MINUTE,
        "iat": now,
        "jti": f'token_id:{str(time.time())}',
        "nbf": now,
        "realm": "stone_bank",
        "sub": CLIENT_ID,
    }


def authenticate():
    auth_token = generate_token(auth_claims())
    data = {
        "client_assertion_type": "urn:ietf:params:oauth:client-assertion-type:jwt-bearer",
        "client_assertion": auth_token,
        "client_id": CLIENT_ID,
        "grant_type": "client_credentials",
    }

    response = requests.post(
        f"{ACCOUNTS_URL}/auth/realms/stone_bank/protocol/openid-connect/token", data=data)

    return response.json()["access_token"]
```

Neste exemplo, estamos definindo uma função que retorna um dicionário com todos os claims necessários para o token de autenticação. Em seguida, é preciso enviar esse token e mais algumas informações para o nosso serviço de autenticação via POST. 

A biblioteca `requests` foi a escolhida para realizar as requisições HTTP. No parâmetro `data`, envia-se dados no formato  "x-www-form-urlencoded" já que este é o formato esperado pelo servidor de autenticação. Ver [documentação](https://2.python-requests.org/en/master/).

No parâmetro `params` envia-se os dados no formato [Query String](https://en.wikipedia.org/wiki/Query_string), e no parâmetro `headers` informamos o que será enviado no cabeçalho da requisição.

Para facilitar o acesso aos dados da resposta, convertemos o conteúdo para JSON e retornamos o `access_token`.

Para utilizar o token de acesso, é preciso apenas adicionar esse token em um cabeçalho `authorization` com o valor `Bearer TOKEN`. Com isso, já é possível operar na API como é demonstrado mais a frente.

<br>

#### **4. Montando o link de consentimento**


Assim como para o token de autenticação, inicialmente consultamos quais os claims específicos do token de consentimento na [documentação](https://docs.openbank.stone.com.br/docs/consentimento-guides#section-gerando-o-token) e, em seguida, utilizamos a função que construimos para gerar e assinar o token.

Neste caso, vamos um pouco além da geração do token, utilizando uma função para montar o link de consentimento com os três parâmetros especificados na [documentação](https://docs.openbank.stone.com.br/docs/consentimento-guides#section-o-link-de-consentimento-deve-conter-tr-s-par-metros-). 

Resumindo o passo a passo para obter o link do consentimento, é preciso:

1. Montar os claims para o token;
2. Criar o token;
3. Montar o link.


```JSON
def consent_claims():
    now = int(time.time())
    return {
        "aud": "accounts-hubid@openbank.stone.com.br",
        "client_id": CLIENT_ID,
        "exp": now + 2 * HOUR,
        "iat": now,
        "iss": CLIENT_ID,
        "jti": str(time.time()),
        "nbf": now,
        "redirect_uri": REDIRECT_URI,
        "session_metadata": {"sid": f'key:{time.time()}'},
        "type": "consent",
    }
  
  
 def consent_token():
    return generate_token(consent_claims())
  
 def consent_link():
    return f"{ACCOUNTS_URL}/consentimento?client_id={CLIENT_ID}&jwt={consent_token()}"
```


O resultado será um link válido por duas horas. Ele pode ser acessado e testado através do navegador.

Observe que alguns detalhes podem ser adaptados de acordo com as necessidades específiicas de controle de tokens da sua aplicação.

Um exemplo é parâmetro `jti`, que faz parte dos claims e atua como um identificador do token. No código acima, é utilizada apenas uma string com o timestamp do momento como forma de garantir sua unicidade. Para sua aplicação é possível utilizar outros valores de forma a facilitar a identificação do token.

Outro exemplo é o campo `session_metadata`, para o qual passamos um dicionário único apenas por ser um campo obrigatório. Neste caso não temos intenção de controlar a sessão, mas a desenvolvedora pode utilizá-lo para esta finalidade, passando valores que se encaixam nas suas necessiades.

<br>


#### **5. Utilizando a API**

Utilizando seu `access_token` já é possível acessar as funcionalidades da API, de acordo com o que a sua aplicação tem permissão de fazer. Para ter permissão de criar transações em contas de usuários, ou até de visualizar seus dados, é preciso obter consentimento do dono da conta. Isso é possível enviando o link construído no passo anterior para a usuária, para que ela possa dar acesso à conta.


##### **Consultando as contas às quais a aplicação parceira tem acesso**

Através da API é possível, por exemplo, consultar a quais contas você tem acesso, tanto no caso de você ser uma aplicação parceira com consentimento para acessar contas, quanto no caso de você ser proprietário de alguma conta.

Para isso, é preciso apenas consultar o endpoint [Consultar Todas Contas às Quais Se Tem Acesso](https://docs.openbank.stone.com.br/reference#consultar-todas-contas-%C3%A0s-quais-a-usu%C3%A1ria-tem-acesso), utilizando seu `access_token` no campo do botão `Try It`.

Outra forma de acessar esse endpoint é realizando uma chamada para nossa API, enviando seu `access_token` em um header. Abaixo podemos observar isso em um exemplo de função que poderia ser utilizada para realizar essa consulta.


```JSON
def operational_accounts(access_token, pagination_params={}):
    url = f"{API_URL}/accounts"
    params = {"paginate": "true", **pagination_params}
    
    response = requests.get(
        url,
        params=params,
        headers={"authorization": f'Bearer {access_token}'}
    ).json()
    return response['data']
```



Analisando o código acima, podemos chegar às seguintes conclusões:

Observe que temos dois parâmetros na função `operational_accounts`: `access_token` e `pagination_params`.

- `access_token` : É o resultado de uma autenticação bem sucedida. Sempre que uma aplicação parceira se autenticar receberá um token de acesso, cuja validade é informada em seus claims;

- `pagination_params`: A maior parte dos nossos endpoints utilizam uma [paginação padrão](https://docs.openbank.stone.com.br/reference#pagina%C3%A7%C3%A3o). Isso permite realizar requisições HTTP de forma mais prática, além de poupar consumo de rede.

E, por fim, obtem-se como resposta uma lista das contas às quais a aplicação tem acesso.

{{% pageinfo %}}
**Padrões da Nossa API**

Seguimos alguns padrões para alguns tipos de dados em toda a nossa API. [Aqui](https://docs.openbank.stone.com.br/reference#data-e-hora) se encontram alguns destes padrões.

{{% /pageinfo %}}

<br>


#### **Criando transferências em uma conta**


Outra funcionalidade é a criação de transferências, tanto entre contas Stone como também de uma conta Stone para contas em outros bancos.

Assim como no caso anterior e de forma padrão para nossos endpoints, para acessá-los é preciso apenas obter permissão de acesso através do consentimento ou ser o próprio dono da conta, e provar isso enviando seu `access_token` em um header. As informações de permissões de um sujeito são armazenadas em seu `access_token`.

O exemplo a seguir foi construído considerando uma aplicação com acesso a pelo menos duas contas, e que a primeira conta tem saldo suficiente para a transferência.


```JSON
def internal_transfer(token, params):
    url = f'{API_URL}/internal_transfers'

    response = requests.post(url,
                             json=params,
                             headers={
                                 "authorization": f'Bearer {token}'
                             }).json()

    return response
  
token = authenticate()
  
accounts = operational_accounts(token)
  
internal_transfer_params = {
    "amount": 1000,
    "account_id": accounts[0]["id"],
    "target": {
        "account": {"account_code": accounts[1]["account_code"]}
    }
}
  
response = internal_transfer(token, internal_transfer_params)
print(response.json())
```


Ocorrendo tudo bem, você receberá como retorno as informações da transferência recém-criada. Em caso de erro como, por exemplo, por saldo insuficiente, receberá como retorno uma mensagem de erro.


{{< alert title="Success" >}}

```JSON
{
  "amount": 1000,
  "approval_expired_at": null,
  "approved_at": null,
  "approved_by": null,
  "cancelled_at": null,
  "created_at": "2019-07-29T13:40:05Z",
  "created_by": "application:92b5f9aa-9552-45f4-86cb-c0331c9178a2",
  "description": "",
  "failed_at": null,
  "failure_reason_code": null,
  "failure_reason_description": null,
  "fee": 0,
  "finished_at": null,
  "id": "000ebdf8-4acf-4ed2-83e9-f0c7a766ac61",
  "rejected_at": null,
  "rejected_by": null,
  "scheduled_to": null,
  "settled_at": null,
  "status": "CREATED",
  "target": {
    "account": {
      "account_code": "517532"
    },
    "entity": {
      "name": "Severo"
    }
  },
  "target_account_code": "517532",
  "target_account_owner_name": "Severo"
}
```
{{< /alert >}}


{{< alert title="Failure" >}}

```JSON
{"type": "srn:error:not_enough_funds"}
```
{{< /alert >}}

<br>


#### **Conclusão**

Utilizando tokens é possível se autenticar e realizar a solicitação de consentimento em contas de usuários de forma segura.

É preciso utilizar uma biblioteca para gerar e assinar os tokens JWT. A escolha da biblioteca deve ser feita com cuidado pois é preciso ter conhecimento de como utilizá-la corretamente para obter sucesso gerando os tokens.

É interessante também consultar os claims específicos para cada token na sessão adequada da documentação, além de se atentar à necessidade de utilizar sua chave privada e o algoritmo RS256 para assinar seus tokens.

Utilizando o `access_token` e obtendo consentimento, já é possível realizar chamadas na API e acessar suas funcionalidades, como consultar as contas às quais a aplicação tem acesso, consultar o saldo dessas contas e criar transferências.