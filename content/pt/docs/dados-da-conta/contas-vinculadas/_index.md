---
title: "Consultar Conta"
slug: "contas-vinculadas"
excerpt: "Verificar Contas Vinculadas a um Usuário"
hidden: true
draft: true
date: "2018-10-30T18:50:48.203Z"
lastmod: "2019-12-02T22:56:58.205Z"
---
[block:api-header]
{
  "title": "1. Como Consultar Dados de uma Conta"
}
[/block]

Como descrito anteriormente, a `Accounts API` tem como responsabilidade ser um endpoint consultivo de informações da conta de pagamentos da usuária.

Para exemplificar isso, vamos utilizar como exemplo, a consulta dos dados bancários de um determinado *account_id*, neste caso, iremos utilizar o seguinte *id*:

`account_id`:**383debcd-0fcd-47cd-b997-3abe668ca9d0**

Note que todo o *id* consultado na `Accounts API` será o *account_id*.
[block:callout]
{
  "type": "success",
  "title": "Para tal requisição oferecemos o endpoint abaixo:",
  "body": "**GET**\n\nhttps://sandbox-api.openbank.stone.com.br/api/v1/accounts/id"
}
[/block]
Neste exemplo, ao realizarmos um **GET** no endpoint **/accounts/id**, substituindo o **{id}** pelo *account_id* do cliente, iremos retornar os dados básicos de uma determinada conta. Veja a requisição abaixo:
[block:code]
{
  "codes": [
    {
      "code": "curl --request GET \\\n  --url https://sandbox-api.openbank.stone.com.br/api/v1/accounts/813b953f-76fd-4776-ac25-b38bb8fce90b \\\n  --header 'authorization: Bearer {token}'",
      "language": "curl"
    },
    {
      "code": "require 'uri'\nrequire 'net/http'\n\nurl = URI(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/813b953f-76fd-4776-ac25-b38bb8fce90b\")\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\n\nrequest = Net::HTTP::Get.new(url)\nrequest[\"authorization\"] = 'Bearer {token}'\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "var data = JSON.stringify(false);\n\nvar xhr = new XMLHttpRequest();\nxhr.withCredentials = true;\n\nxhr.addEventListener(\"readystatechange\", function () {\n  if (this.readyState === this.DONE) {\n    console.log(this.responseText);\n  }\n});\n\nxhr.open(\"GET\", \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/813b953f-76fd-4776-ac25-b38bb8fce90b\");\nxhr.setRequestHeader(\"authorization\", \"Bearer {token}\");\n\nxhr.send(data);",
      "language": "javascript"
    },
    {
      "code": "import requests\n\nurl = \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/813b953f-76fd-4776-ac25-b38bb8fce90b\"\n\nheaders = {'authorization': 'Bearer {token}'}\n\nresponse = requests.request(\"GET\", url, headers=headers)\n\nprint(response.text)",
      "language": "python"
    },
    {
      "code": "var client = new RestClient(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/813b953f-76fd-4776-ac25-b38bb8fce90b\");\nvar request = new RestRequest(Method.GET);\nrequest.AddHeader(\"authorization\", \"Bearer {token}\");\nIRestResponse response = client.Execute(request);",
      "language": "csharp"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "API Reference:",
  "body": "https://docs.openbank.stone.com.br/v1.0/reference#get_accounts-id"
}
[/block]
 
## 1.1 Analisando o JSON

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"account_code\": \"895115\",\n  \"id\": \"383debcd-0fcd-47cd-b997-3abe668ca9d0\",\n  \"branch_code\": \"1\",\n  \"owner_id\": \"user:813b953f-76fd-4776-ac25-b38bb8fce90b\",\n  \"owner_document\": \"31455351881\",\n  \"owner_name\": \"John Doe\"\n}",
      "language": "json"
    }
  ]
}
[/block]
A diferença deste endpoint para o endpoint */accounts* realizado na [Overview Accounts API](doc:overview) é que consultamos apenas um *id* específico, retornando os dados de apenas uma conta bancária. Já o */accounts* lista todas as contas vinculadas a um determinado operador/parceiro, se tornando também o endpoint responsável por consultar o *account_id* da usuária.
[block:api-header]
{
  "title": "2. Como Consultar o Saldo"
}
[/block]
O saldo de uma conta, representa o montante em reais do dinheiro que a usuária tem disponível para uso.

Aproveitando que já sabemos o *account_id* que devemos consultar, iremos verificar o saldo da  conta do exemplo acima.
[block:callout]
{
  "type": "success",
  "title": "Para isso utilize o seguinte endpoint:",
  "body": "**GET**\n\nhttps://sandbox-api.openbank.stone.com.br/api/v1/accounts/id/balance"
}
[/block]
Ao realizarmos um **GET** no endpoint **/accounts/{id}/balance**, substituindo o **{id}** pelo *account_id* do cliente, o mesmo irá retornar o saldo de uma determinada conta. Veja o exemplo:
[block:code]
{
  "codes": [
    {
      "code": "curl --request GET \\\n  --url https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/balance \\\n  --header 'authorization: Bearer {token}'",
      "language": "curl"
    },
    {
      "code": "require 'uri'\nrequire 'net/http'\n\nurl = URI(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/balance\")\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\n\nrequest = Net::HTTP::Get.new(url)\nrequest[\"authorization\"] = 'Bearer {token}'\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "var data = JSON.stringify(false);\n\nvar xhr = new XMLHttpRequest();\nxhr.withCredentials = true;\n\nxhr.addEventListener(\"readystatechange\", function () {\n  if (this.readyState === this.DONE) {\n    console.log(this.responseText);\n  }\n});\n\nxhr.open(\"GET\", \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/balance\");\nxhr.setRequestHeader(\"authorization\", \"Bearer {token}\");\n\nxhr.send(data);",
      "language": "javascript"
    },
    {
      "code": "import requests\n\nurl = \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/balance\"\n\nheaders = {'authorization': 'Bearer {token}'}\n\nresponse = requests.request(\"GET\", url, headers=headers)\n\nprint(response.text)",
      "language": "python"
    },
    {
      "code": "var client = new RestClient(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/balance\");\nvar request = new RestRequest(Method.GET);\nrequest.AddHeader(\"authorization\", \"Bearer {token}\");\nIRestResponse response = client.Execute(request);",
      "language": "csharp"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "API Reference:",
  "body": "https://docs.openbank.stone.com.br/v1.0/reference#get_accounts-id-balance"
}
[/block]
## 2.1 Analisando o JSON

Abaixo temos um JSON da resposta dessa requisição:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"balance\": 9998\n}",
      "language": "json"
    }
  ]
}
[/block]
Note que a variável  _balance_ retornou um total de **9998**, isso corresponde a **R$ 99,98** reais da conta do usuário.
[block:api-header]
{
  "title": "3. Como Consultar o Extrato"
}
[/block]
O extrato de uma conta é representado pelas últimas movimentações financeiras de entrada e saída de dinheiro.


[block:callout]
{
  "type": "success",
  "title": "Para realizar a consulta de extrato utilize o seguinte endpoint:",
  "body": "**GET**\n\nhttps://sandbox-api.openbank.stone.com.br/api/v1/accounts/id/statement"
}
[/block]
Considerando a conta da usuária, faremos a chamada abaixo:
[block:code]
{
  "codes": [
    {
      "code": "curl --request GET \\\n  --url https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/statement \\\n  --header 'authorization: Bearer {token}'",
      "language": "json"
    },
    {
      "code": "require 'uri'\nrequire 'net/http'\n\nurl = URI(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/statement\")\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\n\nrequest = Net::HTTP::Get.new(url)\nrequest[\"authorization\"] = 'Bearer {token}'\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "var data = JSON.stringify(false);\n\nvar xhr = new XMLHttpRequest();\nxhr.withCredentials = true;\n\nxhr.addEventListener(\"readystatechange\", function () {\n  if (this.readyState === this.DONE) {\n    console.log(this.responseText);\n  }\n});\n\nxhr.open(\"GET\", \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/statement\");\nxhr.setRequestHeader(\"authorization\", \"Bearer {token}\");\n\nxhr.send(data);",
      "language": "javascript"
    },
    {
      "code": "import requests\n\nurl = \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/statement\"\n\nheaders = {'authorization': 'Bearer {token}'}\n\nresponse = requests.request(\"GET\", url, headers=headers)\n\nprint(response.text)",
      "language": "python"
    },
    {
      "code": "var client = new RestClient(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts/383debcd-0fcd-47cd-b997-3abe668ca9d0/statement\");\nvar request = new RestRequest(Method.GET);\nrequest.AddHeader(\"authorization\", \"Bearer {token}\");\nIRestResponse response = client.Execute(request);",
      "language": "csharp"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "API Reference:",
  "body": "https://docs.openbank.stone.com.br/v1.0/reference#get_accounts-id-statement"
}
[/block]

## 3.1 Analisando o JSON

Abaixo temos um JSON da resposta dessa requisição:
[block:code]
{
  "codes": [
    {
      "code": "[\n  {\n    \"amount\": 78920,\n    \"created_at\": \"2018-10-16T14:08:53Z\",\n    \"id\": \"cb49d1a5-3f9d-4274-ae5b-de5a7c0d4cfe\",\n    \"operation\": \"credit\",\n    \"type\": \"external\",\n    \"counter_party\": {\n      \"account\": {\n        \"institution\": \"654874\",\n        \"account_code\": \"98898743\",\n        \"branch_code\": \"9875\",\n        \"institution_name\": \"Banco do Brasil S.A.\"\n      },\n      \"entity\": {\n        \"name\": \"Heriberto Marcelo\",\n        \"document\": \"60107999021\",\n        \"document_type\": \"cpf\"\n      }\n    }\n  },\n  {\n    \"amount\": 1000,\n    \"created_at\": \"2018-10-16T15:08:47Z\",\n    \"id\": \"96849628-d6d6-4a7a-86ff-22b3264fca4c\",\n    \"operation\": \"credit\",\n    \"type\": \"internal\",\n    \"status\": \"FINISHED\",\n    \"description\": \"Devolvendo aquele dinheiro.\",\n    \"counter_party\": {\n      \"account\": {\n        \"institution\": \"16501555\",\n        \"account_code\": \"000018\",\n        \"branch_code\": \"1\",\n        \"institution_name\": \"STONE PAGAMENTOS S.A.\"\n      },\n      \"entity\": {\n        \"name\": \"Reinaldo Nathália\",\n        \"document\": \"60107999021\",\n        \"document_type\": \"cpf\"\n      }\n    }\n  }\n]",
      "language": "json"
    }
  ]
}
[/block]
Note que na resposta acima, foram feitas duas transferências, uma interna e uma externa. Ambas com as suas particularidades de retorno.

Obs: O extrato é divido por tipos de movimentação. É possível consultar qual foi a movimentação pelo `type` da resposta, no caso acima podemos notar que tivemos duas movimentações, uma transferência internal (`type:internal`) e uma transferência externa (`type:external), ambas com campos de resposta diferentes.
