---
title: "Criar Novo Pedido de Conta de Pagamento"
excerpt: "Cria um novo usuário e sua organização, caso não exista."
date: 2020-05-04T18:32:40-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 1
draft: false
description: >
---

---
<br>

Realiza o cadastro de conta de pagamento para pessoa física ou pessoa jurídica.

---
<br>

O cadastro é feito de forma assíncrona de forma a permitir:

 - Uma maior velocidade de resposta;
 - Resiliência a falhas a partir de retentativas. Com isso conseguimos evitar que erros ocasionais como falhas de infraestrutura afete a nossa retenção de clientes no cadastro.



```
POST https://sandbox-api.openbank.stone.com.br/api/v1/applications/{global_id}/signups
```

<br>


#### **Request Parameters**

---
<br>

##### **PATH PARAMETER**
---
<br>

**global_id*** `string`<br>
Identifica o tipo e o identificador de um recurso.<br>
Para aplicações o global_id corresponde a "application:CLIENT_ID", onde CLIENT_ID é o id da aplicação.


```json
{
   "global_id": "application:7fc3a55f-b6a3-4b92-a07a-4166bg392341"
}
```
<br>

##### **HEADERS**
---

<br>

**x-stone-idempotency-key** `string`

**authorization** `string`<br>
Para gerar o token [acesse aqui](/docs/guias/integracao/autenticacao).

```json
{
  "x-stone-idempotency-key": "25478963571458", 
  "authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJhY2NvdW50cy1odWJpZEBvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJuYmYiOjE2MTU0NzI9GjAsInNlc3Npb25fbWV0YWRhdGEiOnsiZW1wcmVzYVpXIjoxLCJjaGF2ZVpXIjoienciLCJwcm9kdWNhbyI6ZmFsc2V9LCJpc3MiOiJkODAzMDQ4ZC03MzA2LTQxNTYtYjNlMS1hNjlkMWNiZjQ3ODEiLCJyZWRpcmVjdF91cmkiOiJodHRwOi8vbG9jYWxob3N0Ojg1ODUvc3RvbmViYW5rL2NvbnNlbnRyZWRpcmVjdCIsInR5cGUiOiJjb25zZW50IiwiZXhwIjoxNjE1NDc5OTI5LCJpYWJ3OjE2MTU0NzI3MTksImp0aSI6Ijk0NTlmMjhhLTQ5NDEtNDA2Zi05YjExLWFmMjdhMWQ2MzEyMCJ9.SptDNxVKp5W_9B" 
}
```

<br>

##### **REQUEST BODY**

---
<br>

Consiste no envio dos dados do usuário e opcionalmente da organização que iremos solicitar o pedido de criação de conta de pagamento.

Como esse endpoint trafega dados sensíveis, é necessário criptografar a requisição enviando um JWE (JSON Web Encryption), este corresponde a um JWT criptografado.

O corpo da requisição terá o formato:

```json
{
    "jwe": "jwe_body"
}
```
<br>

**Como gerar o JWE:**

<br>

1- Requisite as chaves de criptografia:
 
```
GET https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys
```
2- Extraia da resposta a chave que tenha como chave valor "use: enc", essa corresponde a chave para criptografar (enc/encrypt).

3- Usar uma biblioteca de criptografia passando o payload (dados do usuário, veja abaixo no [Schema](/docs/referencia-da-api/dados-da-conta/criar-nova-conta-de-pagamento/#schema) ), a chave pública encontrada no item 2.

Segue um exemplo de como gerar um JWE em Python:

<br>

**Python**

```python
import requests
import json
from jwcrypto import jwe, jwk
from jwcrypto.common import json_encode
import sys


def generate_jwe(payload):
  key = get_public_key()
  public_key = jwk.JWK()
  public_key = public_key.from_json(json.dumps(key))

  encrypted = jwe.JWE(payload.encode("utf-8"), recipient=public_key, protected={
      "alg": "RSA-OAEP-256",
      "enc": "A256GCM",
      "kid": key["kid"],
  })

  return encrypted.serialize(compact=True)


def get_public_key():
  response = requests.get(
      "https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys")

  for key in response.json()["keys"]:
      if key["use"] == "enc":
          return key

payload = json_encode({
    'user': {
      'document': '44946137033',
      'document_type': 'cpf',
      'full_name': 'José da Silva',
      'email': 'gabriela.andrade+30@stone.com.br'
    }
  })
jwe = generate_jwe(payload)
print(jwe)
```


##### Exemplo de preenchimento do payload com envio dos dados da organização:


```Json
{
  "user": {
    "document": "52762077044",
    "document_type": "cpf",
    "full_name": "Fulano da Silva",
    "email": "any_valid_non_burner_email1231@gmail.com"
  },
  "organization": {
    "document": "67946893000133",
    "document_type": "cnpj"
  }
}
```


<br>

##### **Schema**
---
<br>

**object:**

   - **user*** `object`

     - **document*** `string`

     - **document_type*** `string`

     - **full_name*** `string`

     - **email*** `string`


   - **organization:*** `string` or `Object`

     - **document*** `string`

     - **document_type*** `string`

     - **full_name** `string`

     - **email** `string`

     - **metadata** `object`




<br>

##### **Responses**
---

```json
202 Accepted
```

{{% pageinfo %}}
**Observação**

Por ser uma chamada assíncrona temos como resposta o código de status 202 e o id do pedido de requisição. Esse pode ser utilizado pela [API de consulta](/docs/referencia-da-api/dados-da-conta/consultar-dados-do-pedido-da-conta-de-pagamento) do pedido de requisição para verificar os metadados e o estado atual do cadastro do cliente.
{{% /pageinfo %}}

<br>

##### Example


```json
{
  "id": "9c6197d8-4b76-422c-ba81-11fb1ca97313"
}
```



