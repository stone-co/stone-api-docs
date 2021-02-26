---
title: "Testando a API"
slug: "testando-a-api-guides"
hidden: false
date: "2019-05-28T18:05:07.002Z"
lastmod: "2019-07-10T18:16:57.794Z"
weight: 4
---

---

<br>

Nossa API é baseada em [REST](https://pt.wikipedia.org/wiki/REST) e a comunicação é feita utilizando métodos de [requisição HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) (**GET**, **POST**, **PUT**, **DELETE**, etc)

Para todos os endpoints, o formato esperado para o `content_type` é sempre `application/json`. A URL base para a API em Sandbox é `https://sandbox-api.openbank.stone.com.br/api/v1`

Abaixo temos um exemplo de uma requisição válida para a API em Sandbox, utilizando a ferramenta `curl`:


```JSON
curl --request GET \ 
  
  --url https://sandbox-api.openbank.stone.com.br/api/v1/institutions/197
```


O retorno das chamadas na API será, por padrão, um objeto do tipo JSON. A chamada anterior tem a seguinte resposta:

```JSON
{
  "ispb_code":"16501555",
  "name":"Stone Pagamentos S.A.",
  "number_code":"197",
  "short_name":"STONE PAGAMENTOS S.A."
}
```


A chamada abaixo é usada para enviar uma TED. Nesse caso, adicionamos como _headers_ o tipo de conteúdo como sendo `application/json` e a autenticação via `Bearer token`, como discutida na sessão de autenticação. 


```JSON
curl --request POST \
  
  --url https://sandbox-api.openbank.stone.com.br/api/v1/external_transfers \
  --header 'Content-Type: application/json' \
  --header 'authorization: Bearer {token}' \
  --data '{"amount":3000,"target":{"account":{"account_code":"654321","branch_code":"1234","institution_code":"260"},"entity":{"cpf":"05971627007","name":"Nome do destinatário"}},"account_id":"f49a9d13-18dc-4811-b286-edd168a428b2"}'
```

Essas requisições geram respostas, conforme podemos ver abaixo:

```JSON
{  
   "amount":16600,
   "approval_expired_at":null,
   "approved_at":"2019-06-07T18:57:57Z",
   "approved_by":"user:b2b80e9a-7412-47de-b303-2f70f3c8e279",
   "cancelled_at":null,
   "created_at":"2019-06-07T18:57:57Z",
   "created_by":"user:b2b80e9a-7412-47de-b303-2f70f3c8e279",
   "delayed_to_next_business_day":false,
   "failed_at":null,
   "fee":0,
   "finished_at":null,
   "id":"05e2950b-ff0c-4b8f-aa5f-7055bb8bc6f1",
   "refund_reason_code":null,
   "refund_reason_description":null,
   "refunded_at":null,
   "rejected_at":null,
   "rejected_by":null,
   "scheduled_to_effective":null,
   "scheduled_to_requested":null,
   "settled_at":null,
   "status":"APPROVED",
   "target":{  
      "account":{  
         "account_code":"1241441",
         "branch_code":"1241",
         "institution_code":"00000000",
         "institution_name":"Banco do Brasil S.A."
      },
      "entity":{  
         "cpf":"37818425098",
         "name":"fulano novo"
      }
   }
}
```

<br>

#### **Homologando sua Integração**


Uma vez que o seu sistema que integra na API do Stone OpenBank está pronto e testado em Sandbox, você vai passar pelo processo de Homologação antes de ir para Produção.
Esse processo consiste em executar todas as ações que a sua Aplicação tem autorização para fazer, numa sequência definida e com o acompanhamento da equipe da Stone. Esse processo visa garantir que sua Aplicação vá funcionar conforme o esperado e que possui acesso a todos os recursos necessários. 
Qualquer problema encontrado durante esta fase deve ser resolvido antes de prosseguir com a subida para Produção.
