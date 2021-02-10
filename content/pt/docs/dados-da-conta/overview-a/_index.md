---
title: "Overview Accounts API"
slug: "overview-a"
hidden: true
draft: true
createdAt: "2018-10-26T20:45:55.912Z"
updatedAt: "2019-12-02T22:56:58.205Z"
---
[block:api-header]
{
  "title": "Descrição do modelo de contas"
}
[/block]
Em nossa modelagem da conta de pagamentos, temos o conceito de o *user_id* e o *account_id*. Esse conceito pode ser definido da seguinte maneira:

* `user_id`: se refere ao identificador do perfil da cliente, contendo informações de dados cadastrais da usuária, como por exemplo, nome, apelido e CPF.
* `account_id`: se refere ao identificador da conta do cliente, contendo dados da conta de pagamentos.

Essa modelagem foi feita considerando que antes de uma `user_id` se tornar um `account_id`, ela passa por um processo de *due diligence*, analisando informações de risco desse cliente, antes  dela ter una Conta de pagamentos Stone.
[block:callout]
{
  "type": "info",
  "body": "Todo o processo de Due Diligience da usuária fica sob responsabilidade da Stone, e se aprovado, será gerado um `account_id` para a usuária"
}
[/block]

[block:api-header]
{
  "title": "1. Verificar o Account_id"
}
[/block]
A **Accounts API** possuí como objetivo ser um endpoint consultivo, na qual, trará como respostas informações bancárias sobre a conta do usuário.

O `user_id`retorna dados cadastrais do usuário enquanto o `account_id`retorna dados em relação a conta do usuário.
[block:callout]
{
  "type": "success",
  "title": "Para isso, vamos utilizar o seguinte endpoint da Accounts API para consultar esse account_id:",
  "body": "**GET**\n\nhttps://sandbox-api.openbank.stone.com.br/api/v1/accounts"
}
[/block]
Obs: A *account_id*, será a mesma utilizada para outras requisições da **Accounts API**

Veja o exemplo da chamada:
[block:code]
{
  "codes": [
    {
      "code": "curl --request GET \\\n  --url https://sandbox-api.openbank.stone.com.br/api/v1/accounts \\\n  --header 'authorization: Bearer {token}'",
      "language": "curl"
    },
    {
      "code": "require 'uri'\nrequire 'net/http'\n\nurl = URI(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts\")\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\n\nrequest = Net::HTTP::Get.new(url)\nrequest[\"authorization\"] = 'Bearer {token}'\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "var data = JSON.stringify(false);\n\nvar xhr = new XMLHttpRequest();\nxhr.withCredentials = true;\n\nxhr.addEventListener(\"readystatechange\", function () {\n  if (this.readyState === this.DONE) {\n    console.log(this.responseText);\n  }\n});\n\nxhr.open(\"GET\", \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts\");\nxhr.setRequestHeader(\"authorization\", \"Bearer {token}\");\n\nxhr.send(data);",
      "language": "javascript"
    },
    {
      "code": "import requests\n\nurl = \"https://sandbox-api.openbank.stone.com.br/api/v1/accounts\"\n\nheaders = {'authorization': 'Bearer {token}'}\n\nresponse = requests.request(\"GET\", url, headers=headers)\n\nprint(response.text)",
      "language": "python"
    },
    {
      "code": "var client = new RestClient(\"https://sandbox-api.openbank.stone.com.br/api/v1/accounts\");\nvar request = new RestRequest(Method.GET);\nrequest.AddHeader(\"authorization\", \"Bearer {token}\");\nIRestResponse response = client.Execute(request);",
      "language": "csharp"
    }
  ]
}
[/block]
## 1.1 Analisando o JSON


Temos como exemplo:
[block:code]
{
  "codes": [
    {
      "code": "[\n  {\n    \"account_code\": \"NÚMERO_DA_CONTA_DA_USUÁRIA\",\n    \"id\": \"NÚMERO_DE_IDENTIFICAÇÃO_DA_CONTA\",\n    \"branch_code\": \"NÚMERO_DA_AGÊNCIA\",\n    \"owner_id\": \"ID_DA_USUARIA\",\n    \"owner_document\": \"DOCUMENTO\",\n    \"owner_name\": \"NOME COMPLETO\"\n  },\n]",
      "language": "json"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Uma mesma usuária pode possuir mais de uma conta vinculada, sendo elas uma conta de pessoa física e diversas contas de pessoa jurídica."
}
[/block]

[block:api-header]
{
  "title": "Outras requisições"
}
[/block]
* [Verificar contas vinculadas a um usuário](https://docs.openbank.stone.com.br/v1.0/docs/verificar-contas-vinculadas-a-um-usu%C3%A1rio)
* [Dados da conta do usuário](https://docs.openbank.stone.com.br/v1.0/docs/dados-b%C3%A1sicos-do-usu%C3%A1rio)
* [Saldo da conta do usuário](https://docs.openbank.stone.com.br/v1.0/docs/saldo-da-conta-do-usu%C3%A1rio)
* [Extrato da conta do usuário](https://docs.openbank.stone.com.br/v1.0/docs/extrato-da-conta-do-usu%C3%A1rio)
* [Taxa cobrada por tipo de pagamento](https://docs.openbank.stone.com.br/v1.0/docs/taxa-cobrada-por-tipo-de-pagamento)