---
title: "Buscar dados do QRCode"
linkTitle: "Buscar dados do QRCode"
lastmod: 2021-04-01T18:00:00-03:00
weight: 1
draft: false
description: >
---  
---
<br>

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/outbound_pix_payments/brcodes
```

A API para criação de um Pix é a mesma, independente se você deseja enviar um Pix via inserção manual de dados ou via chave. Se o pagamento for iniciado por meio da leitura de um QR Code, você vai precisar obter os dados do QR Code primeiro, para depois criar o Pix.

E esse é o objetivo desse endpoint.

<br>

#### **HEADERS**
---
<br>

**authorization*** `string`
<br> Bearer token de autenticação

<br>

Exemplo:

```json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

<br>

#### **BODY PARAMS**
---
<br>

O body deve conter a string do QRCode obtida a partir da imagem ou copia e cola. 
Para QRCode do tipo dinâmico com multa, juros, desconto é necessário informar os campos `payment_date` e `owner_account`

<br>

**brcode*** `string`

**owner_account** `string` <br> Identificador do usuário da conta

**payment_date** `string` 
<br> Data de pagamento da cobrança com vencimento 
<br>Format: YYYY/MM/DD


<br>

Body:

```json
{
  "brcode": "00020126580014br.gov.bcb.pix0136123e4567-e12b-12d1-a456-4266554400005204000053039865802BR5913Fulano de Tal6008BRASILIA62070503***63041D3D"
}
```
<br>



<br>

##### **Responses**
---

<br>

A resposta varia de acordo com o tipo de QR Code que você está lendo, que pode ser um QR Code Estático, um QR Code Dinâmico de pagamento imediato ou um QR Code Dinâmico com multa, juros, desconto. Esse último ainda não é suportado, entra em vigor no Brasil em maio, já estamos desenvolvendo.

<br>

###### **Payload retornado ao consultar um QR Code estático**
---


```
200 OK
```

```json
{
  "type": "static",
  "static": {
    "key": "14413050762",
    "key_type": "phone",
    "transaction_id": "4DE46328260C11EB91C04049FC2CA371",
    "amount": 111
  }
}
```

<br>

###### **Payload retornado ao consultar um QR Code dinâmico**
---

```
200 OK
```

```json
{
  "type": "dynamic",
  "dynamic": {
    "created_at": "2020-11-13T23:59:49Z",
    "requested_at": "2020-11-28T03:15:39Z",
    "expiration": 86400,
    "key": "14413050762",
    "customer": {
      "name": "Fulano CO",
      "document": "50443756000183",
      "document_type": "cnpj"
    },
    "additional_data": [
      {
        "key": "title",
        "value": "description"
      }
    ],
    "revision": 0,
    "request_for_payer": "do something",
    "status": "CANCELLED_BY_BENEFICIARY",
    "transaction_id": "4DE46328260C11EB91C04049FC2CA371",
    "amount": 111
  }
}
```
<br>


###### **Retornado quando o QRCode não pode ser obtido**
---

```
400
```

```json
{
  "type": "srn:error:bad_request"
}
```

<br>

###### **Retornado quando o tipo do QRCode não foi suportado ainda**
---
<br>

Ex.: QRCode com vencimento, juros e multa.

```
501
```

```json
{
  "type": "srn:error:brcode_not_supported"
}
```