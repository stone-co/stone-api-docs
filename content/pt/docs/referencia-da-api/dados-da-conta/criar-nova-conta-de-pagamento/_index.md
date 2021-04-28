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



```http
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


```Json
{
   "global_id": "application:7fc3a55f-b6a3-4b92-a07a-4166bg392341"
}
```
<br>

##### **HEADERS**
---

<br>

**x-stone-idempotency-key** `string`

**x-stone-subject-token** `string`<br>
Para gerar o token [acesse aqui](/docs/guias/integracao/autenticacao).

**authorization** `string`<br>
Mesmo valor do campo x-stone-subject-token.

```Json
{
  "x-stone-idempotency-key": "25478963571458", 
  "x-stone-subject-token": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJhY2NvdW50cy1odWJpZEBvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJuYmYiOjE2MTU0NzI9GjAsInNlc3Npb25fbWV0YWRhdGEiOnsiZW1wcmVzYVpXIjoxLCJjaGF2ZVpXIjoienciLCJwcm9kdWNhbyI6ZmFsc2V9LCJpc3MiOiJkODAzMDQ4ZC03MzA2LTQxNTYtYjNlMS1hNjlkMWNiZjQ3ODEiLCJyZWRpcmVjdF91cmkiOiJodHRwOi8vbG9jYWxob3N0Ojg1ODUvc3RvbmViYW5rL2NvbnNlbnRyZWRpcmVjdCIsInR5cGUiOiJjb25zZW50IiwiZXhwIjoxNjE1NDc5OTI5LCJpYWJ3OjE2MTU0NzI3MTksImp0aSI6Ijk0NTlmMjhhLTQ5NDEtNDA2Zi05YjExLWFmMjdhMWQ2MzEyMCJ9.SptDNxVKp5W_9B",
  "authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJhY2NvdW50cy1odWJpZEBvcGVuYmFuay5zdG9uZS5jb20uYnIiLCJuYmYiOjE2MTU0NzI9GjAsInNlc3Npb25fbWV0YWRhdGEiOnsiZW1wcmVzYVpXIjoxLCJjaGF2ZVpXIjoienciLCJwcm9kdWNhbyI6ZmFsc2V9LCJpc3MiOiJkODAzMDQ4ZC03MzA2LTQxNTYtYjNlMS1hNjlkMWNiZjQ3ODEiLCJyZWRpcmVjdF91cmkiOiJodHRwOi8vbG9jYWxob3N0Ojg1ODUvc3RvbmViYW5rL2NvbnNlbnRyZWRpcmVjdCIsInR5cGUiOiJjb25zZW50IiwiZXhwIjoxNjE1NDc5OTI5LCJpYWJ3OjE2MTU0NzI3MTksImp0aSI6Ijk0NTlmMjhhLTQ5NDEtNDA2Zi05YjExLWFmMjdhMWQ2MzEyMCJ9.SptDNxVKp5W_9B" 
}
```

<br>

##### **REQUEST BODY**

---
<br>

Consiste nos dados do usuário e opcionalmente na organização que iremos cadastrar.

Como esse endpoint trafega dados sensíveis, é necessário criptografar a requisição enviando um JWE (JSON Web Encryption), este corresponde a um JWT criptografado.

O corpo da requisição terá o formato:

```Json
{
    "jwe": "jwe_body"
}
```
<br>

**Como gerar o JWE:**

<br>

1- Requisite as chaves de criptografia:
 
```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys
```
2- Extraia da resposta a chave que tenha como chave valor "use: enc", essa corresponde a chave para criptografar (enc/encrypt).

3- Com essa chave utilize uma implementação de Javascript Object Signing and Encryption (JOSE) para criptografar o conteúdo a ser enviado na requisição.
O conteúdo a ser criptografado segue o schema mencionado mais abaixo na documentação.
Esse passo varia de acordo com a linguagem utilizada na sua implementação, abaixo oferecemos alguns exemplos.

<br>

**Python**

```python
  from jwcrypto import jwk, jwe
  from jwcrypto.common import json_encode

  payload = json_encode({
    'user': {
      'document': '44946137033',
      'document_type': 'cpf',
      'full_name': 'José da Silva',
      'email': 'josesilva@example.com'
    }
  })

  public_key = {} # chave extraída no passo 2
  encoded_key = json_encode({
    'alg': 'RSA-OAEP-256',
    'enc': 'A256GCM',
    'kid': public_key['kid']
  })

  # Instancia a chave
  jwk_key = jwk.JWK(**public_key)

  # Criptografa o payload do signup
  jwetoken = jwe.JWE(payload, enc)
  jwetoken.add_recipient(jwk_key)

  # Converte a chave para o formato JWT compacto
  jwe_body = jwetoken.serialize(compact=True)
```

**Javascript**

```javascript
  import * as jose from 'node-jose'

  payload = {
    'user': {
      'document': '44946137033',
      'document_type': 'cpf',
      'full_name': 'José da Silva',
      'email': 'josesilva@example.com'
    }
  }

  publicKey = {} # chave extraída no passo 2
  
  jwe_body = jose.JWK.asKey(publicKey).then(key =>
      jose.JWE.createEncrypt(
        {
          format: 'compact',
          fields: { alg: 'RSA-OAEP-256', enc: 'A256GCM' }
        },
        key
      )
        .update(jose.util.asBuffer(JSON.stringify(payload)))
        .final()
        .then(result => result)
  )

```

##### Exemplo de preenchimento do payload:


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


4- Utilizamos o algoritmo de criptografia 'RSA-OAEP-256' com o método criptografia 'A256GCM' e o JWE deve ser enviado no formato compacto.

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

```Json
202 Accepted
```

{{% pageinfo %}}
**Observação**

Por ser uma chamada assíncrona temos como resposta o código de status 202 e o id do pedido de requisição. Esse pode ser utilizado pela [API de consulta](/docs/referencia-da-api/dados-da-conta/consultar-dados-do-pedido-da-conta-de-pagamento) do pedido de requisição para verificar os metadados e o estado atual do cadastro do cliente.
{{% /pageinfo %}}

<br>

##### Example


```Json
{
  "id": "9c6197d8-4b76-422c-ba81-11fb1ca97313"
}
```



