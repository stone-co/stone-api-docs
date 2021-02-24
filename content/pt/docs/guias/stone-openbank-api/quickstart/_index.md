---
title: "Quickstart"
slug: "quickstart-guides"
hidden: false
createdAt: "2019-05-28T18:25:23.542Z"
updatedAt: "2019-07-15T20:15:50.410Z"
weight: 2
---

---
<br>

Faça a sua primeira movimentação financeira de teste seguindo esses três passos:

1 - Cadastre-se no **Stone Open Bank API**;

2 - Escolha a sua linguagem/ferramenta preferida;

3 - Crie uma transação.


### 1 - Cadastre-se no Stone Open Bank"

<br>

**ClientID**


Obtenha o seu *Access Token*, enviando um e-mail para nosso time de Parcerias através de parcerias@openbank.stone.com.br.
Somente com o *Access Token* em mãos você consegue realizar as [autenticações](https://docs.openbank.stone.com.br/docs/autenticacao-guides) necessárias para realizar as [chamadas](https://docs.openbank.stone.com.br/v1.0/reference) na **Stone Open Bank API**. 

O time de Parcerias do Stone Open Bank irá te enviar um formulário para preenchimento com os dados sobre seu projeto e posteriormente irá gerar um *ClientID*. Uma vez cadastrado e com o seu *ClientID* em mãos, você poderá realizar o processo de [autenticação da aplicação](https://docs.openbank.stone.com.br/docs/autenticacao-guides), que permitirá que obtenha-se o *Access Token*. Este processo de [autenticação ](https://docs.openbank.stone.com.br/docs/autenticacao-guides) consiste nas seguintes etapas: 

<br>

**Geração de um token que contenha:**

- client_id: identificador enviado pelo time de suporte OpenBank;
- sub: igual ao client_id;
- realm: "stone_bank";
- aud: https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank;
- exp: horário da expiração do token em segundos;
- nbf: horário da geração do token em segundos.

<br>

**Obtenção de access e refresh tokens**

Uma vez obtido o token, deve-se configurar os seguintes parâmetros e realizar a seguinte chamada:
```
**POST** https://sandbox-accounts.openbank.stone.com.br/auth/realms/stone_bank/protocol/openid-connect/token

content-type x-www-form-urlencoded
```
- client_id: identificador enviado pelo time de suporte OpenBank;
- grant_type: sempre será client_credentials;
- client_assertion: token obtido na etapa de geração do token;
- client_assertion_type: sempre será "urn:ietf:params:oauth:client-assertion-type:jwt-bearer".

<br>

Obtido sucesso, o servidor retornará o *access_token* e o *refresh_token* da conta da Aplicação.


{{% pageinfo %}}
**O fluxo acima é um exemplo de como iniciar a sua integração com a Stone Open Bank API.**

Para detalhes sobre o processo de integração, consultar a página [Como Integrar com a API](https://docs.openbank.stone.com.br/docs/autenticacao-guides).
    
{{% /pageinfo %}}



### 2 - Escolha a sua linguagem

<br>

A **Stone Open Bank** disponibiliza sua infraestrutura por meio de uma [API RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) e respostas em [JSON](http://www.json.org/).


{{% pageinfo %}}
**Todas as requisições são feitas no endpoint base:**

https://sandbox-api.openbank.stone.com.br/api/v1
    
{{% /pageinfo %}}




### 3 - Crie uma TED

<br>

Depois de se cadastrar, pegar o seu token de teste e escolher a sua linguagem já é possível começar a movimentar a sua conta de teste! 

Para realizar uma movimentação de TED teste, por exemplo, você pode fazer uma chamada na **Stone Open Bank API**. Pode-se observar um exemplo de chamada teste abaixo:


{{< alert title="cURL" >}}

```JSON
curl --request POST \ 
  
  --url https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers \
  --header 'Content-Type: application/json' \
  --header 'authorization: Bearer {token}' \
  --data '{"amount":3000,"target":{"account":{"account_code":"654321","branch_code":"1234","institution_code":"260"},"entity":{"cpf":"05971627007","name":"Nome do destinatário"}},"account_id":"f49a9d13-18dc-4811-b286-edd168a428b2"}'
```

{{< /alert >}}




{{< alert title="Ruby" >}}

```JSON
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

{{< /alert >}}



{{< alert title="JavaScript" >}}

```JSON
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

{{< /alert >}}




{{< alert title="Python" >}}

```JSON
import requests

url = "https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers"

payload = "{\"amount\":10050,\"target\":{\"account\":{\"account_code\":\"1456879\",\"branch_code\":\"0633\",\"institution_code\":\"379\"},\"entity\":{\"cpf\":\"67385417752\",\"name\":\"Vitoria Silva Correia\"}},\"account_id\":\"200568\"}"
headers = {'authorization': 'Bearer {token}'}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

{{< /alert >}}



{{< alert title="C#" >}}

```JSON
var client = new RestClient("https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers");
var request = new RestRequest(Method.POST);
request.AddHeader("authorization", "Bearer {token}");
request.AddParameter("undefined", "{\"amount\":10050,\"target\":{\"account\":{\"account_code\":\"1456879\",\"branch_code\":\"0633\",\"institution_code\":\"379\"},\"entity\":{\"cpf\":\"67385417752\",\"name\":\"Vitoria Silva Correia\"}},\"account_id\":\"200568\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

{{< /alert >}}



Caso queira saber mais sobre as chamadas disponíveis na nossa API, consulte nossos endpoints em [API Reference](https://docs.openbank.stone.com.br/v1.0/reference).



### 4 - Construindo o seu App

<br>

Com a resposta gerada pela requisição da TED acima, você poderá elaborar uma tela exibindo as informações da transferência realizada. Por exemplo, para construir a tela abaixo:


![imagem_tela_de_transferencia](/home/bruno/Documentos/stone-api-docs/content/pt/docs/guias/stone-openbank-api/quickstart/Tela-Transferencia.png)



É utilizada a requisição citada 3º passo, tendo como resposta o seguinte JSON:


```JSON
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


{{% pageinfo %}}
**Entenda mais sobre a Transfers API e a sua requisição de TED**

Detalhes sobre a Transfers API se encontram na página [Transferir para Outros Bancos](https://docs.openbank.stone.com.br/reference#transferir-para-outros-bancos).
{{% /pageinfo %}}


