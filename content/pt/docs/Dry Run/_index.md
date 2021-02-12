---
title: "Overview Dry Run"
linkTitle: "Overview Dry Run"
hidden: true
createdAt: "2018-10-19T20:57:05.070Z"
updatedAt: "2019-12-02T22:56:58.216Z"
weight: 4

---

### Conceito
<br>

O termo dry run significa “ensaio completo” em qualquer tipo de atividade antes de fato executá-la.
Disponibilizamos uma API de Dry Run para simulações de transferências internas, externas e pagamentos, com o objetivo de garantir que a informação da requisição feita esteja correta.

Desta forma é necessário que haja uma requisição para a API de Dry Run, **antes** de enviar 
uma requisição à API que efetuará a transação iminente. 

<br>

---


### Como fazer um Dry Run

<br>
Com os dados da transferência interna, você poderá fazer uma tela de confirmação dentro do seu próprio aplicativo antes mesmo de fazer a transferência interna.

```JSon
{
  "type": "success",
  "title": "Para isso você precisa fazer a seguinte chamada na API:",
  "body": "**POST**\n\nhttps://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers"
}
```

Nesse caso, é enviado o mesmo payload de uma transferência interna para este endpoint, conforme exemplo abaixo:

```JSon
{
  "codes": [
    {
      "code": "curl --request POST \\\n  --url https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers \\\n  --data \n  '{\"amount\":1896,\n  \"account_id\":\"404d26a4-8a6b-4a96-b3ef-ba3fbb58e327\",\n  \"target_account_code\":\n  \"889745\"\n  }'",
      "language": "curl"
    },
    {
      "code": "var request = require(\"request\");\n\nvar options = { method: 'POST',\n  url: 'https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers',\n  body: \n   { amount: 7335,\n     account_id: '404d26a4-8a6b-4a96-b3ef-ba3fbb58e327',\n     target_account_code: '889745' },\n  json: true };\n\nrequest(options, function (error, response, body) {\n  if (error) throw new Error(error);\n\n  console.log(body);\n});",
      "language": "javascript"
    },
    {
      "code": "require 'uri'\nrequire 'net/http'\n\nurl = URI(\"https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers\")\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\n\nrequest = Net::HTTP::Post.new(url)\nrequest.body = \"{\\\"amount\\\":7335,\\\"account_id\\\":\\\"404d26a4-8a6b-4a96-b3ef-ba3fbb58e327\\\",\\\"target_account_code\\\":\\\"889745\\\"}\"\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "import requests\n\nurl = \"https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers\"\n\npayload = \"{\\\"amount\\\":7335,\\\"account_id\\\":\\\"404d26a4-8a6b-4a96-b3ef-ba3fbb58e327\\\",\\\"target_account_code\\\":\\\"889745\\\"}\"\nresponse = requests.request(\"POST\", url, data=payload)\n\nprint(response.text)",
      "language": "python"
    },
    {
      "code": "var client = new RestClient(\"https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers\");\nvar request = new RestRequest(Method.POST);\nrequest.AddParameter(\"undefined\", \"{\\\"amount\\\":7335,\\\"account_id\\\":\\\"404d26a4-8a6b-4a96-b3ef-ba3fbb58e327\\\",\\\"target_account_code\\\":\\\"889745\\\"}\", ParameterType.RequestBody);\nIRestResponse response = client.Execute(request);",
      "language": "csharp"
    },
    {
      "code": "POST https://sandbox-api.openbank.stone.com.br/api/v1/dry_run/internal_transfers\n{\n\t\"amount\":987654321,\n\t\"account_id\":\"404d26a4-8a6b-4a96-b3ef-ba3fbb58e327\",\n\t\"target_account_code\":\"123456789\"\n}",
      "language": "json",
      "name": "JSON Payload"
    }
  ]
}
```

Essa requisição retorna informações que permitem verificar a transferência antes de ser realizada. Alguns exemplos de campos retornados que podem gerar informações úteis:

* `fee`: taxa da transação
* `target_account_owner_name`: nome do dono da conta destino

```JSon
{
  "type": "info",
  "title": "Para os outros endpoints de dry-run consultar:",
  "body": "[Transferência Interna](https://docs.openbank.stone.com.br/v1.0/reference#post_dry-run-internal-transfers)\n[Transferência Externa](https://docs.openbank.stone.com.br/v1.0/reference#post_dry-run-external-transfers)\n[Pagamentos](https://docs.openbank.stone.com.br/v1.0/reference#post_dry-run-payments)"
}
```










