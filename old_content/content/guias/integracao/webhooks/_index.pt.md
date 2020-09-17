---
title: "Webhooks"
date: 2020-05-14T14:48:28-03:00
lastmod: 2020-05-14T14:48:28-03:00
weight: "7"
draft: false
---

A ocorrência de certos eventos pode ser importante para iniciar um processamento na plataforma do parceiro. Por isso, utilizamos webhooks para notificá-lo da ocorrência destes eventos.

Para sua utilização, é preciso que sua aplicação tenha cadastrada no formulário a URI para a qual enviaremos um POST com os dados do evento. O parceiro deverá se preparar para lidar com cada evento de forma adequada.

Realizamos 50 tentativas de envio dos webhooks.

#### Os eventos que geram notificações são:

| Tipo de evento                               | Descrição                                                                                                      |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| barcode_payment_invoice_created              | Representa a criação/emissão de um boleto.                                                                     |
| barcode_payment_invoice_registered           | Representa o registro de um boleto.                                                                            |
| barcode_payment_invoice_payment_promissed    | Representa que o pagamento do boleto foi acolhido em alguma instituição.                                       |
| barcode_payment_invoice_settled              | Representa a entrada do valor do boleto na conta do beneficiário.                                              |
| cash_in_barcode_payment                      | Representa o recebimento do pagamento de um boleto.                                                            |
| cash_in_card_payment                         | Representa o recebimento de pagamentos de cartão de crédito, cartão de débito ou de antecipação de pagamentos. |
| cash_in_payment_refund                       | Representa o reembolso de um pagamento mal sucedido.                                                           |
| cash_in_internal_transfer                    | Representa o recebimento de uma transferência interna.                                                         |
| cash_in_external_transfer                    | Representa o recebimento de uma transferência externa.                                                         |
| cash_in_external_transfer_refund             | Representa o reembolso de uma transferência externa mal sucedida.                                              |
| cash_out_internal_transfer                   | Representa a criação de uma transferência interna.                                                             |
| cash_out_internal_transfer_failed            | Representa a falha na criação de uma transferência interna.                                                    |
| cash_out_internal_transfer_scheduled         | Representa o agendamento de uma transferência interna.                                                         |
| cash_out_internal_transfer_scheduled_failed  | Representa a falha no agendamento de uma transferência interna.                                                |
| cash_out_internal_transfer_approved          | Representa a aprovação de uma transferência interna.                                                           |
| cash_out_internal_transfer_cancelled         | Representa o cancelamento de uma transferência interna.                                                        |
| cash_out_internal_transfer_rejected          | Representa a rejeição de uma transferência interna.                                                            |
| cash_out_internal_transfer_finished          | Representa a finalização de uma transferência interna.                                                         |
| cash_out_internal_transfer_expired           | Representa a expiração de uma transferência interna.                                                           |
| cash_out_external_transfer                   | Representa a criação de uma transferência externa.                                                             |
| cash_out_external_transfer_failed            | Representa a falha na criação de uma transferência externa.                                                    |
| cash_out_external_transfer_scheduled         | Representa o agendamento de uma transferência *externa*.                                                       |
| cash_out_external_transfer_scheduled_failed  | Representa a falha no agendamento de uma transferência externa.                                                |
| cash_out_external_transfer_approved          | Representa a aprovação de uma transferência externa.                                                           |
| cash_out_external_transfer_cancelled         | Representa o cancelamento de uma transferência externa.                                                        |
| cash_out_external_transfer_rejected          | Representa a rejeição de uma transferência externa.                                                            |
| cash_out_external_transfer_finished          | Representa a finalização de uma transferência externa.                                                         |
| cash_out_external_transfer_expired           | Representa a expiração de uma transferência externa.                                                           |
| cash_out_external_transfer_execution_started | Representa o início da execução de uma transferência externa.                                                  |
| cash_out_payment                             | Representa a criação de um pagamento.                                                                          |
| cash_out_payment_failed                      | Representa a falha na criação de um pagamento.                                                                 |
| cash_out_payment_scheduled                   | Representa o agendamento de um pagamento.                                                                      |
| cash_out_payment_scheduled_failed            | Representa a falha no agendamento de um pagamento.                                                             |
| cash_out_payment_approved                    | Representa a aprovação de um pagamento.                                                                        |
| cash_out_payment_cancelled                   | Representa o cancelamento de um pagamento.                                                                     |
| cash_out_payment_rejected                    | Representa a rejeição de um pagamento.                                                                         |
| cash_out_payment_finished                    | Representa a finalização de um pagamento.                                                                      |
| cash_out_payment_expired                     | Representa a expiração de um pagamento.                                                                        |
| cash_out_payment_execution_started           | Representa o início da execução de um pagamento.                                                               |
| consent_requested                            | Representa a confirmação do pedido de consentimento por parte do user.                                         |


#### O header das notificações segue a seguinte estrutura:

```json5
x-stone-webhook-event-id: "930bbd6d-0c7a-4fe4-8b50-4b82a20cb847"
x-stone-webhook-event-type: "cash_out_internal_transfer"
```

#### O payload da notificações segue a seguinte estrutura:

| Campo                | Descrição                                                                                                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| env                  | Especifica de qual ambiente partiu o evento. Valores possíveis: `sandbox` ou `production`.                                                                                                      |
| event_type           | Especifica qual tipo de evento disparou a notificação. Veja os valores possíveis [aqui](https://docs.openbank.stone.com.br/docs/webhooks-guides#section-os-eventos-que-geram-notificacoes-sao). |
| id                   | É o identificador da notificação.                                                                                                                                                               |
| event_notified_at    | É a hora em que a notificação está sendo enviada.                                                                                                                                               |
| event_happened_at    | É a hora em que o evento ocorreu.                                                                                                                                                               |
| target_data          | Objeto com as informações detalhadas do recurso que gerou o evento. Apesar de ter campo variáveis sempre conterá o campo `account_id`.                                                          |
| target_detail_uri    | É o endereço onde se pode consultar os detalhes do recurso.                                                                                                                                     |
| target_id            | É o identificador do recurso que gerou o evento.                                                                                                                                                |
| target_statement_uri | É o endereço da entrada no extrato referente ao recurso.                                                                                                                                        |
| target_type          | É o tipo do recurso.                                                                                                                                                                            |

{{< notice info >}}
**Inclusão de campos**
<br>A implementação não deve ser strict no parser do payload. Ao longo do tempo os payloads podem sofrer a inclusão de campos.
{{< /notice >}}

##### Exemplo:

```json5
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

#### Trabalhando com Webhooks

##### Webhooks Seguros

Nossa API envia webhooks de forma segura para evitar que eles sejam abertos e/ou alterados. Isso é feito em duas etapas:

1. Assinatura do conteúdo usando uma das nossas [chaves públicas](https://api.openbank.stone.com.br/api/v1/discovery/keys).
2. Ciframento do resultado usando a chave pública do destinatário.

##### Como eu posso abrir de forma segura o conteúdo de um webhook?

Para poder visualizar o conteúdo de um webhook é necessário fazer o caminho inverso:

1. Usar sua chave privada para poder decifrar o conteúdo. O resultado é um token JWT assinado com a nossa chave;
2. Verificar a assinatura do token com a nossa chave pública.

##### 1 - Decifrando o conteúdo do webhook

O webhook irá chegar com um payload parecido com esse:

```json5
{
  "encrypted_body": "xxxxxxxxxxxxxx conteúdo cifrado"
}

```

O valor do campo "encrypted_body" é um token no formato JWE (JSON Web Encryption) compacto. Esse formato é um padrão e várias linguagens possuem bibliotecas prontas para ele.

O algoritmo utilizado é: **RSA-OAEP-256** com **A256GCM**. Para decifrar o conteúdo é necessário uma biblioteca que suporte estes algoritmos como:

- [JavaScript](https://github.com/square/js-jose)
- [Java](https://bitbucket.org/b_c/jose4j/wiki/Home)
- [Erlang/Elixir](https://hexdocs.pm/jose/JOSE.html)
- [Go](https://github.com/square/go-jose)

A chave a ser utilizada tem que ser a **chave privada** par da **chave pública** usada na autenticação da aplicação.

##### 2 - Verificando a assinatura do conteúdo do webhook

Até este momento deciframos apenas um conteúdo que pode ser gerado por qualquer um que tenha acesso a chave pública da aplicação.

Nós utilizamos a assinatura do conteúdo em token JWS (JSON Web Signing) compacto como uma outra camada de verificação de segurança no conteúdo do webhook.

Esse token possui em seus "claims" (alegações) o conteúdo do webhook. Para garantir que ele foi gerado pela Stone, você deve validar a assinatura dele consultando nossas chaves públicas de assinatura.

As chaves públicas da Stone estão publicadas [aqui](https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys).

Repare que cada chave possui um *kid* (key ID) e um *use* (sig ou enc). O token JWS possui um header que diz qual é o id da chave usada para assiná-lo. Assim, é necessário, em primeiro lugar, garantir que o token foi assinado com uma chave que está publicada pela Stone.

O algoritmo que usamos será *sempre RS256*. Há uma lista de bibliotecas que tratam de assinatura de token em [jwt.io](https://jwt.io/).

#### Segurança

É importante seguir os dois passos aqui: tanto decifrar quanto verificar a assinatura. Isso irá garantir que não apenas geramos algo que não pode ser lido por alguém que *não possui* a chave pública quanto que nosso conteúdo foi assinado pela Stone.

Também aconselhamos cuidado na configuração do cliente que irá consultar as nossas chaves. Certifique-se que ele não está vulnerável a servidores intermediários propositalmente mal configurados. Um exemplo comum é um servidor configurado para protocolos conhecidamente falhos.

Sempre que em dúvida, consulte nossa API com os IDs dos dados no conteúdo do webhook.

Mais informações sobre JavaScript Object Signing and Encryption, como JWTs, JWEs, JWSs, [aqui](https://www.ca.com/pt/blog-latam/os-beneficios-de-jwtjwsjwe-no-designs-de-apis.html).
