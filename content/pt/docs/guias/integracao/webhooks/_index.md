---
title: "Webhooks"
slug: "webhooks-guides"
hidden: false
date: "2019-07-29T21:31:30.337Z"
lastmod: "2021-02-01T22:57:33.698Z"
weight: 7
---

---
<br>

A ocorrência de certos eventos pode ser importante em diversos fluxos na integração de uma aplicação com a API OpenBank. Por isso, utilizamos webhooks para notificar as aplicações integradas da ocorrência destes eventos.

Para sua utilização, é preciso que a aplicação tenha cadastrado no formulário a URI para a qual enviaremos um POST com os dados do evento. A aplicação deverá estar preparada para lidar com cada evento de forma adequada.

Ao enviar um webhook, esperamos receber uma resposta do range 200 que indica o sucesso no recebimento dessa notificação por parte da sua aplicação. Caso a resposta seja um código diferente do range 200, encaramos como falha no recebimento do webhook e repetimos o envio até receber um sucesso ou batermos o número máximo de 50 tentativas no envio de um evento.

A aplicação irá receber webhooks dos eventos que acontecerem na(s) conta(s) sobre as quais ela opera dado o escopo de funcionalidades sobre o qual foi dado consentimento. Vale lembrar que os webhooks serão enviados independente se o evento for via API ou via APP.


{{% pageinfo %}}
**Virada em Produção**

É imprescindível que a aplicação esteja recebendo e tratando de forma adequada todos os tipos de webhook referente as funcionalidades que implementou.

{{% /pageinfo %}}

<br>

#### **Os eventos que geram notificações são:**


##### **Emissão de Boleto:**


| Tipo de Evento                               | Descrição                                                                 |
| -------------------------------------------- | ------------------------------------------------------------------------- |
| barcode_payment_invoice_created              | Representa a criação/emissão de um boleto.                                |
| barcode_payment_invoice_registered           | Representa o registro de um boleto.                                       |
| barcode_payment_invoice_payment_promissed    | Representa que o pagamento do boleto foi acolhido em alguma instituição.  |
| barcode_payment_invoice_settled              | Representa que pagamento do boleto foi confirmado.                        |
| cash_in_barcode_payment                      | Representa a entrada do valor do boleto na conta do beneficiário.         | 


##### **Pagamento de Boleto:**

| Tipo de Evento                               | Descrição                                                                 |
| -------------------------------------------- | ------------------------------------------------------------------------- |
| cash_in_payment_refund                       | Representa o reembolso de um pagamento mal sucedido.                      |
| cash_out_payment                             | Representa a criação de um pagamento.                                     |
| cash_out_payment_failed                      | Representa a falha na criação de um pagamento.                            |
| cash_out_payment_scheduled                   | Representa o agendamento de um pagamento.                                 |
| cash_out_payment_scheduled_failed            | Representa a falha no agendamento de um pagamento.                        |
| cash_out_payment_approved                    | Representa a aprovação de um pagamento.                                   |
| cash_out_payment_execution_started           | Representa o início da execução de um pagamento.                          |
| cash_out_payment_cancelled                   | Representa o cancelamento de um pagamento.                                |
| cash_out_payment_rejected                    | Representa a rejeição de um pagamento.                                    |
| cash_out_payment_finished                    | Representa a finalização de um pagamento.                                 |
| cash_out_payment_expired                     | Representa a expiração de um pagamento.                                   |


##### **Transferência interna:**

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


##### **Transferência externa:**

| Tipo de Evento                               | Descrição                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| cash_in_external_transfer                    | Representa o recebimento de uma transferência externa.                   | 
| cash_in_external_transfer_refund             | Representa o reembolso de uma transferência externa mal sucedida.        | 
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


##### **Consentimento:**

| Tipo de Evento                               | Descrição                                                                |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| consent_requested                            | Representa a confirmação do pedido de consentimento por parte do user.   |


##### **Abertura de conta:**

| Tipo de Evento                               | Descrição                                               | Exemplo        |
| -------------------------------------------- | --------------------------------------------------------|--------------- |
| sign_up_created                              | Enviado quando é feito o pedido de abertura de conta.   | [A1](/docs/guias/integracao/webhooks/A1.json)                |
| sign_up_status_updated                       | Enviado quando é feito uma atualização dos dados na abertura da conta.        | [A2](/docs/guias/integracao/webhooks/A2.json)   |
| sign_up_resource_details_updated             | Serão enviados diversos webhooks com este tipo de evento de acordo com a evolução da abertura de conta. Ex: `account_created`, `user_email_verified`, ....| [A3](/docs/guias/integracao/webhooks/A3.json) |



<br>

#### **O header das notificações segue a seguinte estrutura:**


```JSON
x-stone-webhook-event-id: "930bbd6d-0c7a-4fe4-8b50-4b82a20cb847"
x-stone-webhook-event-type: "cash_out_internal_transfer"
```


A idempotência de webhooks deverá ser validada no campo 'x-stone-webhook-event-id' disponível no header.

<br>

#### **O payload das notificações segue a seguinte estrutura:**


| Campo                | Descrição                                                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| env                  | Especifica de qual ambiente partiu o evento. Valores possíveis: sandbox ou production.                                               |
| event_type           | Especifica qual tipo de evento disparou a notificação. Veja os valores possíveis [aqui](/docs/guias/integracao/webhooks/#os-eventos-que-geram-notificações-são).                                               |
| id                   | É o identificador da notificação.                                                                                                    |
| event_notified_at    | É a hora em que a notificação está sendo enviada.                                                                                    |
| event_happened_at    | É a hora em que o evento ocorreu.                                                                                                    |
| target_data          | Objeto com as informações detalhadas do recurso que gerou o evento. Apesar de ter campo variáveis sempre conterá o campo account_id. |
| target_detail_uri    | É o endereço onde se pode consultar os detalhes do recurso.                                                                          |
| target_id            | É o identificador do recurso que gerou o evento.                                                                                     |
| target_statement_uri | É o endereço da entrada no extrato referente ao recurso.                                                                             |
| target_type          | É o tipo do recurso.                                                                                                                 |




{{% pageinfo %}}
**Inclusão de campos**

A implementação não deve ser strict no parser do payload. Ao longo do tempo os payloads podem sofrer a inclusão de campos.

{{% /pageinfo %}}



Exemplo:


```JSON
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

#### **Trabalhando com Webhooks**


##### **Webhooks Seguros**

Nossa API envia webhooks de forma segura para evitar que eles sejam abertos e/ou alterados. Isso é feito em duas etapas:

- Assinatura do conteúdo usando uma das nossas [chaves públicas](https://api.openbank.stone.com.br/api/v1/discovery/keys).
- Ciframento do resultado usando a chave pública do destinatário.



##### **Como eu posso abrir de forma segura o conteúdo de um webhook?**

Para poder visualizar o conteúdo de um webhook é necessário fazer o caminho inverso:

1. **Decifrar o conteúdo do webhook** usando sua chave privada. O resultado é um token JWT assinado com a nossa chave;
2. **Verificar a assinatura do token** com a nossa chave pública.

<br>

##### **1 - Decifrar o conteúdo do webhook**

O webhook irá chegar com um payload parecido com esse:


```JSON
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

<br>


##### **2 - Verificar a assinatura do token**


Até este momento deciframos apenas um conteúdo que pode ser gerado por qualquer um que tenha acesso a chave pública da aplicação.

Nós utilizamos a assinatura do conteúdo em token JWS (JSON Web Signing) compacto como uma outra camada de verificação de segurança no conteúdo do webhook.

Esse token possui em seus "claims" (alegações) o conteúdo do webhook. Para garantir que ele foi gerado pela Stone, você deve validar a assinatura dele consultando nossas chaves públicas de assinatura. 

As chaves públicas da Stone estão publicadas [aqui](https://sandbox-api.openbank.stone.com.br/api/v1/discovery/keys).

Repare que cada chave possui um *kid* (key ID) e um *use* (sig ou enc). O token JWS possui um header que diz qual é o id da chave usada para assiná-lo. Assim, é necessário, em primeiro lugar, garantir que o token foi assinado com uma chave que está publicada pela Stone. 

Para não ter que buscar a nossa chave pública a cada validação de assinatura, você pode salvar nossa chave do seu lado (por exemplo, através de um cache), de forma que caso aconteça algum erro na validação você volte a consultar o nosso serviço para buscar a chave pública mais atual. Assim você desonera  sua aplicação sem perder a resiliência a mudanças de chave do nosso lado.

Veja [aqui](https://hexdocs.pm/joken_jwks/JokenJwks.DefaultStrategyTemplate.html#content) as melhores práticas para fazer essa implementação. 

O algoritmo que usamos será *sempre RS256*. Há uma lista de bibliotecas que tratam de assinatura de token em [jwt.io](https://jwt.io/). 



##### **Segurança**

É importante seguir os dois passos aqui: tanto decifrar quanto verificar a assinatura. Isso irá garantir que não apenas geramos algo que não pode ser lido por alguém que *não possui* a chave pública quanto que nosso conteúdo foi assinado pela Stone. 

Também aconselhamos cuidado na configuração do cliente que irá consultar as nossas chaves. Certifique-se que ele não está vulnerável a servidores intermediários propositalmente mal configurados. Um exemplo comum é um servidor configurado para protocolos conhecidamente falhos.

Sempre que em dúvida, consulte nossa API com os IDs dos dados no conteúdo do webhook.

Mais informações sobre JavaScript Object Signing and Encryption, como JWTs, JWEs, JWSs, [aqui](https://www.ca.com/pt/blog-latam/os-beneficios-de-jwtjwsjwe-no-designs-de-apis.html).



##### **Webhooks idempotentes**

No geral um evento, quando recepcionado com sucesso, é enviado apenas uma vez pela Stone, mas é possível que em algum cenário extraordinário um webhook acabe sendo enviado mais de uma vez e por isso desenvolvemos uma lógica de idempotência de eventos. 

Todo webhook gerado pela Stone leva consigo uma chave de idempotência enviada no campo `x-stone-webhook-event-id` do header. 

É importante que essa chave seja sempre salva pela sua aplicação e que a cada novo evento você verifique a idempotência desse evento evitando processar duas vezes um mesmo evento.

