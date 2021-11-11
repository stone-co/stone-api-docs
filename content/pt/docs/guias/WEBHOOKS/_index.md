---
title: "WEBHOOKS"
linkTitle: "WEBHOOKS"
date: 2021-06-28T09:00:00-03:00
lastmod: 2021-08-26T11:00:00-03:00
weight: 6
draft: false
description: >

---

---
<br>

## Overview
---
<br>

A ocorrência de certos eventos pode ser importante em diversos fluxos na integração de uma aplicação com a API Stone Open Banking. Por isso, utilizamos webhooks para notificar as aplicações integradas da ocorrência desses eventos.

Para sua utilização, é preciso que a aplicação tenha cadastrado no [formulário]({{< relref "/docs/guias/stone-open-banking/#testes-em-sandbox">}}) a URI para a qual enviaremos um POST com os dados do evento. A aplicação deverá estar preparada para lidar com cada evento de forma adequada.

Ao enviar um webhook, esperamos receber uma resposta do range 200 que indica o sucesso no recebimento dessa notificação por parte da sua aplicação. Caso a resposta seja um código diferente do range 200, encaramos como falha no recebimento do webhook e repetimos o envio até receber um sucesso ou batermos o número máximo de 50 tentativas no envio de um evento.
Essas tentativas são realizadas ao longo do dia, de forma assíncrona, sem um padrão de horários de tentativas.

A aplicação irá receber webhooks dos eventos que acontecerem na(s) conta(s) sobre as quais ela opera dado o escopo de funcionalidades disponíveis na sua aplicação e também recebem os eventos relacionados às contas sobre as quais foi dado consentimento. 
<br>Vale lembrar que os webhooks serão enviados independente se o evento for via API ou via app.

<br>

{{% pageinfo %}}
**Virada em Produção**

É imprescindível que a aplicação esteja recebendo e tratando de forma adequada todos os tipos de webhook referentes às funcionalidades que implementou.

{{% /pageinfo %}}

<br>

### Eventos que geram notificações
---

<br>

##### **Emissão de Boleto:**

<br>

| Tipo de Evento                               | Descrição                                                                 |
| :-------------------------------------------- | :------------------------------------------------------------------------- |
| [barcode_payment_invoice_created](barcode_payment_invoice_created.json)              | Representa a criação/emissão de um boleto.                                |
| [barcode_payment_invoice_registered](barcode_payment_invoice_registered.json)           | Representa o registro de um boleto.                                       |
| [barcode_payment_invoice_payment_promissed](barcode_payment_invoice_payment_promissed.json)    | Representa que o pagamento do boleto foi acolhido em alguma instituição.  |
| [barcode_payment_invoice_settled](barcode_payment_invoice_settled.json)              | Representa que o pagamento do boleto foi confirmado.                        |
| [barcode_payment_invoice_expired](barcode_payment_invoice_expired.json)              | Representa que o boleto está expirado.                                    |
| [cash_in_barcode_payment](cash_in_barcode_payment.json)                      | Representa a entrada do valor do boleto na conta do beneficiário.         | 
| [inbound_barcode_payment_refunded](inbound_barcode_payment_refunded.json)            | Representa que o pagamento do boleto foi devolvido.         |


<br>

##### **Pagamento de Boletos, Contas e Tributos:**

<br>

| Tipo de Evento                               | Descrição                                                                 |
| -------------------------------------------- | ------------------------------------------------------------------------- |
| cash_in_payment_refund                       | Representa o reembolso de um pagamento malsucedido.                      |
| [cash_out_payment](cash_out_payment.json)                             | Representa a criação de um pagamento.                                     |
| cash_out_payment_failed                      | Representa a falha na criação de um pagamento.                            |
| cash_out_payment_scheduled                   | Representa o agendamento de um pagamento.                                 |
| cash_out_payment_scheduled_failed            | Representa a falha no agendamento de um pagamento.                        |
| [cash_out_payment_approved](cash_out_payment_approved.json)                    | Representa a aprovação de um pagamento.                                   |
| [cash_out_payment_execution_started](cash_out_payment_execution_started.json)           | Representa o início da execução de um pagamento.                          |
| cash_out_payment_cancelled                   | Representa o cancelamento de um pagamento.                                |
| cash_out_payment_rejected                    | Representa a rejeição de um pagamento.                                    |
| [cash_out_payment_finished](cash_out_payment_finished.json) | Representa a finalização de um pagamento.                  |
| cash_out_payment_expired                     | Representa a expiração de um pagamento.                                   |

<br>

##### **Transferência interna:**

<br>

| Tipo de Evento                               | Descrição                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| cash_in_internal_transfer                    | Representa o recebimento de uma transferência interna.                   |  
| cash_out_internal_transfer                   | Representa a criação de uma transferência interna.                       |  
| cash_out_internal_transfer_failed            | Representa a falha na criação de uma transferência interna.              | 
| cash_out_internal_transfer_scheduled         | Representa o agendamento de uma transferência interna.                   | 
| cash_out_internal_transfer_scheduled_failed  | Representa a falha no agendamento de uma transferência interna.          | 
| cash_out_internal_transfer_approved          | Representa a aprovação de uma transferência interna.                     | 
| cash_out_internal_transfer_cancelled         | Representa o cancelamento de uma transferência interna.                  | 
| cash_out_internal_transfer_rejected          | Representa a rejeição de uma transferência interna.                      | 
| cash_out_internal_transfer_finished          | Representa a finalização de uma transferência interna.                   | 
| cash_out_internal_transfer_expired           | Representa a expiração de uma transferência interna.                     |  

<br>

##### **Transferência externa:**

<br>

| Tipo de Evento                               | Descrição                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| cash_in_external_transfer                    | Representa o recebimento de uma transferência externa.                   | 
| cash_in_external_transfer_refund             | Representa o reembolso de uma transferência externa malsucedida.        | 
| cash_out_external_transfer                   | Representa a criação de uma transferência externa.                       | 
| cash_out_external_transfer_failed            | Representa a falha na criação de uma transferência externa.              | 
| cash_out_external_transfer_scheduled         | Representa o agendamento de uma transferência externa.                   | 
| cash_out_external_transfer_scheduled_failed  | Representa a falha no agendamento de uma transferência externa.          | 
| cash_out_external_transfer_approved          | Representa a aprovação de uma transferência externa.                     | 
| cash_out_external_transfer_execution_started | Representa o início da execução de uma transferência externa.            | 
| cash_out_external_transfer_cancelled         | Representa o cancelamento de uma transferência externa.                  | 
| cash_out_external_transfer_rejected          | Representa a rejeição de uma transferência externa.                      | 
| cash_out_external_transfer_finished          | Representa a finalização de uma transferência externa.                   | 
| cash_out_external_transfer_expired           | Representa a expiração de uma transferência externa.                     |

<br>

##### **Pix:**

<br>




| Tipo de Evento                																											    | Descrição                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| [pix_entries_key_created](pix_entries_key_created.json)          									| Representa a criação de uma chave Pix.            |
| [pix_entries_deleted](pix.entries.deleted.json)               										| Representa a deleção de uma chave Pix.            |
| [pix_entries_failed](pix.entries.failed.json)             											| Representa a falha na criação de uma chave Pix.   |
| [pix_entries_claims_waiting_resolution](pix.entries.claims.waiting_resolution.json) 					| Representa que estamos aguardando a resposta da cliente sobre a claim (confirmação ou cancelamento).  |
| [pix_entries_claims_confirmed](pix.entries.claims.confirmed.json)         							| Representa que a cliente confirmou a claim, passando a chave para outra instituição.             |
| [pix_entries_claims_automatically_confirmed_waiting_resolution](pix.entries.claims.automatically_confirmed_waiting_resolution.json) | Representa que a reivindicação de posse foi automaticamente confirmada porque a cliente não respondeu no prazo de 7 dias corridos. |
| [pix_entries_claims_automatically_confirmed](pix.entries.claims.automatically_confirmed.json) 		| Representa que foi realizada a confirmação da reivindicação de posse automaticamente, porque a cliente não respondeu dentro dos 14 dias de prazo. Aqui a reivindicação não pode ser mais cancelada.  |
| [pix_entries_claims_cancelled](pix.entries.claims.cancelled.json)         							| Representa cancelamento da solicitação da claim por parte da cliente, mantendo a chave cadastrada na conta original. |
| [pix_entries_claims_automatically_cancelled](pix.entries.claims.automatically_cancelled.json) 		| Representa cancelamento automático da solicitação de portabilidade, por falta de resposta da cliente nos 7 dias de prazo.   |
| [pix_payment_invoice](pix_payment_invoice.json)														| Representa um QR Code dinâmico imediato.						|
| [pix_payment_invoice_with_due_date](pix_payment_invoice_with_due_date.json)							| Representa um QR Code dinâmico com vencimento, multa, juros, desconto e abatimento.	|
| [pix_invoice_payment_created](pix_invoice_payment_created.json)       								| Representa a criação de um QR Code dinâmico. 	 			   	|
| [pix_invoice_payment_cancelled](pix_invoice_payment_cancelled.json)        							| Representa o cancelamento de um QR Code dinâmico.     		|
| [pix_invoice_payment_paid](pix_invoice_payment_paid.json)          									| Representa o pagamento com sucesso de um QR Code dinâmico.    |
| [inbound_pix_payment](inbound_pix_payment.json)														| Representa um cash-in de Pix.	|
| [pix_inbound_payment_received](pix_inbound_payment_received.json)         							| Representa o recebimento de um cash-in de Pix, podendo estar associado a um QR Code estatático, dinâmico imediato ou dinâmico com vencimento. Essa associação será representada pela presença de um dos seguintes atributos dentro do target_data: <br>- `pix_payment_invoice`: Invoice dinâmica imediata; <br>- `pix_payment_static_invoice`: Invoice estática; <br>- `pix_payment_invoice_with_due_date`: Invoice dinâmica com vencimento, multa, juros, desconto e abatimento.  |
| [pix_refund_payment](pix_refund_payment.json)										| Representa uma devolução (cash-out) associada a um inbound payment (cash-in).		|
| [pix_inbound_payment_refund_created](pix.inbound_payment.refund.created.json)   						| Representa a criação de uma devolução associada a uma transação Pix. Lembrando que estamos falando da devolução (cash-out) de um cash-in.  |
| [pix_inbound_payment_refund_failed](pix.inbound_payment.refund.failed.json)    						| Representa que houve falha na criação da devolução (cash-out) de um cash-in de Pix.    |
| [pix_inbound_payment_refund_money_reserved](pix.inbound_payment.refund.money_reserved.json) 			| Representa a reserva de dinheiro (impacto no saldo da cliente) após a criação com sucesso de uma devolução (cash-out) de um cash-in de Pix.    |
| [pix_inbound_payment_refund_settled](pix.inbound_payment.refund.settled.json)   						| Representa que a devolução (cash-out) de um cash-in de Pix foi realizada com sucesso.            |
| [pix_inbound_payment_refund_reversed](pix.inbound_payment.refund.reversed.json)  					| Representa que a devolução (cash-out) de um cash-in de Pix foi rejeitada.                     |
| [pix_outbound_payment_created](pix_outbound_payment_created.json)         | Representa a criação de um cash-out de Pix.  |
| [pix_outbound_payment_money_reserved](pix_outbound_payment_money_reserved.json)  | Representa a reserva de dinheiro (impacto no saldo da cliente) após a criação com sucesso de um cash-out de Pix. |
| pix_outbound_payment_failed          | Representa a falha na criação de um cash-out de Pix.         |
| pix_outbound_payment_settled         | Representa a liquidação com sucesso de um cash-out de Pix.   |
| pix_outbound_payment_refunded        | Representa a devolução de um cash-out de Pix.   	          |

<br>

##### **Consentimento:**

<br>

| Tipo de Evento               | Descrição                                                                |  
| -----------------------------| ------------------------------------------------------------------------ | 
| [consent_request](exemplo_consent_request.json) | Representa a confirmação do pedido de consentimento por parte do user.   |

<br>

##### **Abertura de conta:**

<br>

| Tipo de Evento                               | Descrição                                                                | 
| -------------------------------------------- | ------------------------------------------------------------------------ |
| [sign_up_created](A1.json)| Representa o pedido de abertura de conta.       | 
| [sign_up_status_updated](A2.json) | Representa quando há uma atualização dos dados na abertura da conta.        |
| [sign_up_resource_details_updated](A3.json) | Representa o envio de diversos webhooks de acordo com a evolução da abertura de conta. Exemplo: `account_created`, `user_email_verified`, ....|

<br>

##### **Link de Pagamento:**

<br>

| Tipo de Evento                               | Descrição                                                                | 
| -------------------------------------------- | ------------------------------------------------------------------------ |
| [order_created](lp_order_created.json)| Representa a criação do link de pagamento. <br>Também é enviado um [segundo webhook](lp_order_created_status_pending.json) desse tipo que representa que o pagador executou o pagamento. <br>Nesse caso, o campo `status` do webhook terá seu valor alterado para `pending`.              | 
| [order_paid](lp_order_paid.json)| Representa o pagamento em si do link de pagamento.   |
| [order_closed](lp_order_closed.json)|  Representa a finalização do link de pagamento.   |

<br>

## Estrutura do header das notificações
---



```
x-stone-webhook-event-id: "930bbd6d-0c7a-4fe4-8b50-4b82a20cb847"
x-stone-webhook-event-type: "cash_out_internal_transfer"
```


A idempotência de webhooks deverá ser validada no campo 'x-stone-webhook-event-id' disponível no header.

<br>

## Estrutura do payload das notificações
---

<br>

| Campo                | Descrição                                                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| env                  | Especifica de qual ambiente partiu o evento. Valores possíveis: sandbox ou production.                                               |
| event_type           | Especifica qual tipo de evento disparou a notificação. Veja os valores possíveis [aqui](#eventos-que-geram-notificações). |
| id                   | É o identificador da notificação.                                                                                                    |
| event_notified_at    | É a hora em que a notificação está sendo enviada.                                                                                    |
| event_happened_at    | É a hora em que o evento ocorreu.                                                                                                    |
| target_data          | Objeto com as informações detalhadas do recurso que gerou o evento. Apesar de ter campos variáveis, sempre conterá o campo account_id. |
| target_detail_uri    | É o endereço onde se pode consultar os detalhes do recurso.                                                                          |
| target_id            | É o identificador do recurso que gerou o evento.                                                                                     |
| target_statement_uri | É o endereço da entrada no extrato referente ao recurso.                                                                             |
| target_type          | É o tipo do recurso.                                                                                                                 |

<br>


{{% pageinfo %}}
**Inclusão de campos**

A implementação não deve ser strict no parser do payload. Ao longo do tempo, os payloads podem sofrer a inclusão de campos.

{{% /pageinfo %}}

<br>

Exemplo:


```json
{
   "env":"sandbox",
   "event_type":"cash_in_internal_transfer",
   "event_happened_at":"2020-05-13T14:58:15Z",
   "event_notified_at":"2020-05-13T14:58:15Z",
   "iat":1589381895,
   "id":null,
   "jti":"2o79sqemde14mv76eo00jsc3",
   "nbf":1589381895,
   "target_data":{
      "account_id":"09c016b2-876a-450a-9f40-316f8e2f8778",
      "amount":1,
      "balance_after":null,
      "balance_before":null,
      "counter_party":{
         "account":{
            "account_code":"841412",
            "branch_code":"1",
            "institution":"16501555",
            "institution_name":"Stone Pagamentos S.A."
         },
         "entity":{
            "name":"Loja Da Maria"
         }
      },
      "created_at":"2020-05-13T14:58:15Z",
      "description":"",
      "id":"54abd61c-3b18-401c-9816-951cbe135149",
      "operation":"credit",
      "status":"FINISHED",
      "type":"internal"
   },
   "target_detail_uri":null,
   "target_id":null,
   "target_statement_uri":"https://sandbox-api.openbank.stone.com.br/api/v1/statement/entries/54abd61c-3b18-401c-9816-951cbe135149",
   "target_type":"internal_transfer"
}
```

<br>

## Trabalhando com Webhooks
---
<br>

### **Webhooks Seguros**

<br>

Nossa API envia webhooks de forma segura para evitar que eles sejam abertos e/ou alterados. Isso é feito em duas etapas:

- Assinatura do conteúdo usando uma das nossas [chaves públicas](https://api.openbank.stone.com.br/api/v1/discovery/keys).
- Ciframento do resultado usando a chave pública do destinatário.


<br>

##### **Como eu posso abrir de forma segura o conteúdo de um webhook?**

<br>

Para poder visualizar o conteúdo de um webhook, é necessário fazer o caminho inverso:

1. **Decifrar o conteúdo do webhook** usando sua chave privada. O resultado é um token JWT assinado com a nossa chave;
2. **Verificar a assinatura do token** com a nossa chave pública.

<br>

##### **1 - Decifrar o conteúdo do webhook**
---

<br>

O webhook irá chegar com um payload parecido com este:


```json
{
  "encrypted_body": "xxxxxxxxxxxxxx conteúdo cifrado"
}
```

O valor do campo "encrypted_body" é um token no formato JWE (JSON Web Encryption) compacto. Esse formato é um padrão e várias linguagens possuem bibliotecas prontas para ele.

O algoritmo utilizado é: **RSA-OAEP-256** com **A256GCM**. Para decifrar o conteúdo, é necessária uma biblioteca que suporte esses algoritmos como:

- [JavaScript](https://github.com/square/js-jose)
- [Java](https://bitbucket.org/b_c/jose4j/wiki/Home)
- [Erlang/Elixir](https://hexdocs.pm/jose/JOSE.html)
- [Go](https://github.com/square/go-jose)

A chave a ser utilizada tem que ser a **chave privada** par da **chave pública** usada na autenticação da aplicação.

Um exemplo para decodificar o webhook pode ser verificado no código em Python abaixo:

```python
from jwcrypto import jwk, jwe
from jwcrypto.common import json_encode
import jwt
import time
import subprocess
import simplejson as json

webhook_response = {"encrypted_body":"eyJhbGciOiJSU0EtT0FFz2C15nwK...kadnFeyS100SDgTPA9pO5GS4_jZw.SwKpGLZ_f2-q-Gw"}

token = webhook_response['encrypted_body']

with open("private-key.pem", "rb") as pemfile:
    jwk_private_key = jwk.JWK.from_pem(pemfile.read())

jwetoken = jwe.JWE()
jwetoken.deserialize(token)
jwetoken.decrypt(jwk_private_key)
payload = jwetoken.payload.decode('utf-8')

jwt_decoded = jwt.decode(payload, options={"verify_signature": False})
jwt_parsed = json_encode(jwt_decoded)

subprocess.run('pbcopy', universal_newlines=True, input=jwt_parsed)
```

<br>


##### **2 - Verificar a assinatura do token**
---

<br>

Até este momento, deciframos apenas um conteúdo que pode ser gerado por qualquer um que tenha acesso à chave pública da aplicação.

Nós utilizamos a assinatura do conteúdo em token JWS (JSON Web Signing) compacto como uma outra camada de verificação de segurança no conteúdo do webhook.

Esse token possui em seus "claims" (alegações) o conteúdo do webhook. Para garantir que ele foi gerado pela Stone, você deve validar a assinatura dele consultando nossas chaves públicas de assinatura. 

As chaves públicas da Stone estão publicadas [aqui](https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys).

Repare que cada chave possui um *kid* (key ID) e um *use* (sig ou enc). O token JWS possui um header que diz qual é o ID da chave usada para assiná-lo. Assim, é necessário, em primeiro lugar, garantir que o token foi assinado com uma chave que está publicada pela Stone. 

Para não ter que buscar a nossa chave pública a cada validação de assinatura, você pode salvar nossa chave do seu lado (por exemplo, através de um cache), de forma que, caso aconteça algum erro na validação, você volte a consultar o nosso serviço para buscar a chave pública mais atual. Assim você desonera  sua aplicação sem perder a resiliência a mudanças de chave do nosso lado.

Veja [aqui](https://hexdocs.pm/joken_jwks/JokenJwks.DefaultStrategyTemplate.html#content) as melhores práticas para fazer essa implementação. 

O algoritmo que usamos será *sempre RS256*. Há uma lista de bibliotecas que tratam de assinatura de token em [jwt.io](https://jwt.io/). 

<br>

##### **Segurança**

<br>

É importante seguir os dois passos aqui: tanto decifrar quanto verificar a assinatura. Isso irá garantir que não apenas geramos algo que não pode ser lido por alguém que *não possui* a chave pública quanto que nosso conteúdo foi assinado pela Stone. 

Também aconselhamos cuidado na configuração do cliente que irá consultar as nossas chaves. Certifique-se de que ele não está vulnerável a servidores intermediários propositalmente mal configurados. Um exemplo comum é um servidor configurado para protocolos conhecidamente falhos.

Sempre que estiver em dúvida, consulte nossa API com os IDs dos dados no conteúdo do webhook.

Mais informações sobre JavaScript Object Signing and Encryption, como JWTs, JWEs, JWSs, [aqui](https://www.ca.com/pt/blog-latam/os-beneficios-de-jwtjwsjwe-no-designs-de-apis.html).

<br>

### **Webhooks idempotentes**

<br>

No geral um evento, quando recepcionado com sucesso, é enviado apenas uma vez pela Stone, mas é possível que em algum cenário extraordinário um webhook acabe sendo enviado mais de uma vez e por isso desenvolvemos uma lógica de idempotência de eventos. 

Todo webhook gerado pela Stone leva consigo uma chave de idempotência enviada no campo `x-stone-webhook-event-id` do header. 

É importante que essa chave seja sempre salva pela sua aplicação e que a cada novo evento você verifique a idempotência desse evento, evitando processar duas vezes um mesmo evento.

<br>

## Endpoint para verificar webhooks enviados
---

<br>

Caso tenha dificuldade para identificar algum webhook enviado pela Stone na URI indicada para receber webhooks, disponibilizamos um endpoint que traz todos os webhooks já enviados para a sua aplicação.

Para acessar, basta fazer o comando abaixo, lembrando que no _header_ deve ser enviado o Bearer token no campo `authorization` e que o client_id é o id da sua aplicação, passado pelo time de integração.

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/applications/application:{{client_id}}/webhooks
```

**Exemplo de Response**

```json
{
  "client_id": "application:de4d224b-3f79-4b4d-8ff5-c1bc475830e5",
  "created_at": "2021-06-02T19:40:24Z",
  "data": {
    "env": "sandbox",
    "event_happened_at": "2021-06-02T19:40:23Z",
    "event_notified_at": "2021-06-02T19:40:24Z",
    "event_type": "cash_out_internal_transfer_finished",
    "id": "7919b78a-630e-4ad4-bb12-91eec729175d",
    "target_data": {
      "account_id": "6745bdf0-7647-40cd-8666-d78bb15fbd38",
      "amount": 4000,
      "approval_expired_at": null,
      "approved_at": "2021-06-02T19:40:23Z",
      "approved_by": "user:24017c13-1f9d-44e4-b4af-007f695cece3",
      "batch_id": null,
      "cancelled_at": null,
      "cancelled_by": null,
      "created_at": "2021-06-02T19:40:23Z",
      "created_by": "user:24017c13-1f9d-44e4-b4af-007f695cece3",
      "description": "",
      "failed_at": null,
      "failure_reason_code": null,
      "failure_reason_description": null,
      "fee": 0,
      "finished_at": "2021-06-02T19:40:23Z",
      "id": "7919b78a-630e-4ad4-bb12-91eec729175d",
      "rejected_at": null,
      "rejected_by": null,
      "scheduled_to": null,
      "settled_at": "2021-06-02T19:40:23Z",
      "status": "FINISHED",
      "target": {
        "account": {
          "account_code": "55382931"
        },
        "entity": {
          "name": ""
        }
      },
      "target_account_code": "55382931",
      "target_account_owner_name": ""
    },
    "target_detail_uri": "https://sandbox-api.openbank.stone.com.br/api/v1/internal_transfers/7919b78a-630e-4ad4-bb12-91eec729175d",
    "target_id": "7919b78a-630e-4ad4-bb12-91eec729175d",
    "target_statement_uri": null,
    "target_type": "internal_transfer_finished"
  }
}
```
