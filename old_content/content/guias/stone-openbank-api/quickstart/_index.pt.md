---
title: "Quickstart"
date: 2020-05-14T10:15:16-03:00
lastmod: 2020-05-14T10:15:16-03:00
weight: "2"
draft: false
---

Faça a sua primeira movimentação financeira de teste seguindo esses três passos:

1. Cadastre-se no **Stone OpenBank API**;
2. Escolha a sua linguagem/ferramenta preferida;
3. Crie uma transação.

#### 1 - Cadastre-se no Stone OpenBank

**ClientID**

Obtenha o seu *Access Token*, por meio deste [formulário](https://docs.google.com/forms/d/e/1FAIpQLSf_qlDh41jfthVn80v4S-HT40_Fr2wbkkGb-KuDrioEqepnXw/viewform). Somente com o *Access Token* em mãos você consegue realizar as [autenticações](https://docs.openbank.stone.com.br/docs/referencia-da-api/autenticacao-guides) necessárias para realizar as [chamadas](https://docs.openbank.stone.com.br/v1.0/reference) na **Stone Open Bank API**.

Após o preenchimento do [formulário](https://docs.google.com/forms/d/e/1FAIpQLSf_qlDh41jfthVn80v4S-HT40_Fr2wbkkGb-KuDrioEqepnXw/viewform), o time de parcerias do Stone Open Bank irá gerar um *ClientID*. Uma vez cadastrado e com a seu *ClientID* em mãos, você poderá realizar o processo de [autenticação da aplicação](https://docs.openbank.stone.com.br/docs/referencia-da-api/autenticacao-guides), que permitirá que obtenha-se o *Acess Token*. Este processo de [autenticação ](https://docs.openbank.stone.com.br/docs/referencia-da-api/autenticacao-guides) consiste nas seguintes etapas:

**Geração de um token que contenha**

- client_id: identificador enviado pelo time de suporte OpenBank;
- sub: igual ao client_id;
- realm: "stone_bank";
- aud: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank;
- exp: horário da expiração do token em segundos;
- nbf: horário da geração do token em segundos.

**Obtenção de access e refresh tokens**

Uma vez obtido o token, deve-se configurar os seguintes parâmetros e realizar a seguinte chamada:
```json5
**POST** https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token
content-type x-www-form-urlencoded
```
- client_id: identificador enviado pelo time de suporte OpenBank;
- grant_type: sempre será client_credentials;
- client_assertion: token obtido na etapa de geração do token;
- client_assertion_type: sempre será "urn:ietf:params:oauth:client-assertion-type:jwt-bearer".

Obtido sucesso, o servidor retornará o *access_token* e o *refresh_token* da conta da Aplicação.
{{< notice info >}}
**O fluxo acima é um exemplo de como iniciar a sua integração com a Stone Open Bank API.**
<br>Para detalhes sobre o processo de integração, consultar a página [Como Integrar com a API](https://docs.openbank.stone.com.br/docs/referencia-da-api/autenticacao-guides).
{{< /notice >}}

#### 2 - Escolha a sua linguagem

A **Stone Open Bank** disponibiliza sua infraestrutura por meio de uma [API RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) e respostas em [JSON](http://www.json.org/).

{{< notice tip >}}
**Todas as requisições são feitas no endpoint base:**
<br>https://sandbox-api.openbank.stone.com.br/api/v1
{{< /notice >}}

#### 3 - Crie uma TED

Depois de se cadastrar, pegar o seu token de teste e escolher a sua linguagem já é possível começar a movimentar a sua conta de teste! Para realizar uma movimentação de TED teste, por exemplo, você pode fazer uma chamada na **Stone Open Bank API**. Pode-se observar um exemplo de chamada teste abaixo:

##### cURL
```shell
curl --request POST \
  --url https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers \
  --header 'Content-Type: application/json' \
  --header 'authorization: Bearer {token}' \
  --data '{"amount":3000,"target":{"account":{"account_code":"654321","branch_code":"1234","institution_code":"260"},"entity":{"cpf":"05971627007","name":"Nome do destinatário"}},"account_id":"f49a9d13-18dc-4811-b286-edd168a428b2"}'
```
    
##### Ruby
```ruby
require 'uri'
require 'net/http'

url = URI("https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["authorization"] = 'Bearer {token}'
request.body = "{\"amount\":10050,\"target\":{\"account\":{\"account_code\":\"1456879\",\"branch_code\":\"0633\",\"institution_code\":\"379\"},\"entity\":{\"cpf\":\"67385417752\",\"name\":\"Vitoria Silva Correia\"}},\"account_id\":\"200568\"}"

response = http.request(request)
puts response.read_body
```

##### Javascript
```javascript
var data = JSON.stringify({
    "amount": 10050,
    "target": {
        "account": {
            "account_code": "1456879",
            "branch_code": "0633",
            "institution_code": "379"
        },
        "entity": {
            "cpf": "67385417752",
            "name": "Vitoria Silva Correia"
        }
    },
    "account_id": "200568"
});

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers");
xhr.setRequestHeader("authorization", "Bearer {token}");

xhr.send(data);
```

##### Python
```python
import requests

url = "https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers"

payload = "{\"amount\":10050,\"target\":{\"account\":{\"account_code\":\"1456879\",\"branch_code\":\"0633\",\"institution_code\":\"379\"},\"entity\":{\"cpf\":\"67385417752\",\"name\":\"Vitoria Silva Correia\"}},\"account_id\":\"200568\"}"
headers = {'authorization': 'Bearer {token}'}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```
##### C#
```csharp
var client = new RestClient("https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers");
var request = new RestRequest(Method.POST);
request.AddHeader("authorization", "Bearer {token}");
request.AddParameter("undefined", "{\"amount\":10050,\"target\":{\"account\":{\"account_code\":\"1456879\",\"branch_code\":\"0633\",\"institution_code\":\"379\"},\"entity\":{\"cpf\":\"67385417752\",\"name\":\"Vitoria Silva Correia\"}},\"account_id\":\"200568\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

Caso queira saber mais sobre as chamadas disponíveis na nossa API, consulte nossos endpoints em [API Reference](https://docs.openbank.stone.com.br/v1.0/reference).

#### 4 - Construindo o seu App

Com a resposta gerada pela requisição da TED acima, você poderá elaborar uma tela exibindo as informações da transferência realizada. Por exemplo, para construir a tela abaixo:

{{< figure src="https://files.readme.io/094d6d3-Tela_Transferncia.png" alt="Tela Transferência.png" width="300">}}

É utilizada a requisição citada 3º passo, tendo como resposta o seguinte JSON:

```json5
{
  "amount": 10050,
  "approved_at": "2018-10-08T22:13:51Z",
  "approved_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "created_at": "2018-10-08T22:13:51Z",
  "created_by": "user:380f9968-8946-4f88-a781-be8b7efc1f90",
  "failed_at": null,
  "fee": 0,
  "id": "79573d4a-613a-4ac7-8970-39c39fc18e5a",
  "refunded_at": null,
  "rejected_at": null,
  "rejected_by": null,
  "settled_at": null,
  "target": {
    "account": {
      "account_code": "1456879",
      "branch_code": "0633",
      "institution_code": "379"
    },
    "entity": {
      "cpf": "67385417752",
      "name": "Vitoria Silva Correia"
    }
  }
}
```

{{< notice tip >}}
**Entenda mais sobre a Transfers API e a sua requisição de TED**
<br>Detalhes sobre a Transfers API se encontram na página [Transferir para Outros Bancos](https://docs.openbank.stone.com.br/reference#transferir-para-outros-bancos).
{{< /notice >}}
