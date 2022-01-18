---
title: "Recarga para Conteúdo Digital"
linkTitle: "Recarga para Conteúdo Digital"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-04-06T18:00:00-03:00
weight: 4
draft: false
description: >
---

---

<br>

#### **Fluxo da recarga**
---

<br>

1) Para efetuar a recarga de créditos para um Conteúdo Digital é necessário que o cliente selecione e escolha o plano/valor. 

2) Após a confirmação da recarga para um Conteúdo Digital, retornamos o **código PIN** ao cliente.

3) Com o código PIN em mãos, **o cliente acessa o site/app do provedor** e resgata os créditos obtidos.

<br>


##### **Provedores disponíveis**
---
<br>

- Spotify;
- Ifood.

<br>

{{% pageinfo %}}
**Atenção**

Para o Spotify os valores oferecidos não são flexíveis;

Quanto ao Ifood a escolha do valor é flexível, com o mínimo de R$1,00 e máximo de R$149,00.

{{% /pageinfo %}}

<br>

{{< alert title="Horário de funcionamento" >}}

<br>


A liquidação é executada no provedor em questões de segundos. O resgate dos créditos é feito ao informar o Código PIN retornado após a confirmação da recarga.


{{< /alert >}}


<br>


#### **Ações a serem executadas para recarga de Conteúdo Digital**
---

<br>

##### **1) Listar todos os provedores de Conteúdo Digital**

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/topups/digital-content/providers
```

###### **Header request**

```json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg",
	"x-stone-idempotency-key": "0001"
}
```

* x-stone-idempotency-key é opcional, para mais informações consulte o [Overview](/docs/referencia-da-api/recargas/overview/#glossário).

###### **Response**

```
200 ok
```

```json
{
  "providers": [
    {
      "name": "Ifood",
      "id": 2153
    },
    {
      "name": "Spotify",
      "id": 2141
    }
  ]
}
```



##### **Possíveis casos de erro ao listar provedores**
##### **401 - Unauthorized**
Caso o cliente não tenha realizado a autenticação.
```json
{
  "type": "srn:error:unauthenticated"
}
```

##### **403 - Forbidden**
Caso o cliente não tenha permissão para listar os provedores.
```json
{
  "type": "srn:error:forbidden"
}
```


<br>

##### **2) Listar todos os valores para o provedor**

```
GET https://sandbox-api.openbank.stone.com.br/api/v1/topups/digital-content/values/{provider-id}
```

###### **Header request**

```json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg",
	"x-stone-idempotency-key": "0001"
}
```

* x-stone-idempotency-key é opcional, para mais informações consulte o [Overview](/docs/referencia-da-api/recargas/overview/#glossário).

###### **Responses**

```
200 ok
```

**- Name: Spotify / id: 2141**

```json
{
  "product": [
    {
      "product_name": "Spotify Pin 17 BRL",
      "value": 1700
    },
    {
      "product_name": "Spotify Pin 50 BRL",
      "value": 5000
    },
    {
      "product_name": "Spotify Pin 100 BRL",
      "value": 10000
    }
  ]
}
```

**- Name: Ifood / id: 2153**

```json
{
  "product": [
    {
      "value": 1000
    }
  ]
}
```

##### **Possíveis casos de erro ao listar valores para o provedor**

##### **400 - Bad Request**

Caso o cliente tenha passado letras no lugar dos números no id do provedor, por exemplo.

```json
{
  "type": "srn:error:invalid_params"
}
```

##### **401 - Unauthorized**
Caso o cliente não tenha realizado a autenticação.
```json
{
  "type": "srn:error:unauthenticated"
}
```

##### **403 - Forbidden**
Caso o cliente não tenha permissão para listar os valores para o provedor.
```json
{
  "type": "srn:error:forbidden"
}
```

<br>

##### **3) Simular uma recarga de Conteúdo Digital**

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/topups/digital-content/dry-run
```

###### **Header request**

```json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg",
	"x-stone-idempotency-key": "0001"
}
```

* x-stone-idempotency-key é opcional, para mais informações consulte o [Overview](/docs/referencia-da-api/recargas/overview/#glossário).

###### **Body Request**

```json
{
  "account_id": "e4043bb5-542b-46f6-bcbc-0e63d37e1c47",
  "amount": 5000,
  "provider_id": "2141"
}
```

###### **Response**

```
202 Accepted
```

```json
{
  "amount": 5000,
  "account_id": "e4043bb5-542b-46f6-bcbc-0e63d37e1c47",
  "provider_id": "2141"
}
```

##### **Possíveis casos de erro ao simular recarga**

##### **400 - Bad Request**

Caso o cliente tenha passado um valor inválido:

```json
{
   "type": "srn:error:invalid_amount",
   "title": "Given amount is less than or equal to zero"
}
```
Caso o cliente não tenha saldo suficiente para realizar a transação:

```json
{
    "type": "srn:error:not_enough_funds"
}
```

Caso o cliente tenha passado letras no lugar dos números no valor da recarga, por exemplo.

```json
{
  "type": "srn:error:invalid_params"
}
```
##### **403 - Forbidden**
Caso o cliente não tenha permissão para realizar a simulação de recarga.
```json
{
  "type": "srn:error:forbidden"
}
```

<br>

##### **4) Executar uma recarga de Conteúdo Digital**

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/topups/digital-content
```

###### **Header request**


```json
{
    "authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg",
    "x-stone-idempotency-key": "0001",
    "x-stone-challenge-solution": "81080d67-aac9-415b-868f-4403243201d3"
}
```

* x-stone-idempotency-key é opcional, para mais informações consulte o [Overview](/docs/referencia-da-api/recargas/overview/#glossário).
* x-stone-challenge-solution é obrigatório,[clique aqui](/docs/referencia-da-api/recargas/fluxo-challenge/) para ter acesso ao *fluxo de autorização do challenge*

###### **Body Request**

```json
{
  "account_id": "e4043bb5-542b-46f6-bcbc-0e63d37e1c47",
  "amount": 5000,
  "provider_id": "2141"
}
```

###### **Response**

```
200 ok
```

```json
{
    "id": "cd5ff1c2-8f7e-4f56-a9d8-241d4cd1a1a8",
    "receipt": "          PROTOCOLO 0002751870\n1          06/04/2021        15:27\nTERM 228005 AGENTE 228005 AUTE 07642\n----------------------------------------\nAUTO 978142                            \n<VIA1>\nESTE CUPOM NAO TEM VALOR FISCAL\nPRODUTO: SPOTIFY\nVALOR: R$  50,00\nPIN: 6365-4427-6400-1327\nSERIE: 00000000\n\nCOMO RESGATAR OS CREDITOS SPOTIFY:\n1. VISITE SPOTIFY.COM/REDEEM\n2. INFORME O PIN DESTE RECIBO\n3. VALIDADE: 12 MESES\nINFORMACOES: WWW.SPOTIFY.COM/GIFT-CARD\n\nAPOS O USO, INUTILIZE ESTE CUPOM\nIS2B - INTEGRATED SOLUTIONS TO BUSINESS\n\n\n\n\n</VIA1>----------------------------------------\n\n",
    "transaction_id": "b6cb2b73-0e30-4a93-9de6-31201628df79",
    "pin": "6365-4427-6400-1327"
}
```

##### **Possíveis casos de erro ao realizar recarga**
##### **400 - Bad Request**

Caso o cliente tenha passado um valor inválido:

```json
{
  "type": "srn:error:invalid_amount",
  "title": "Given amount is less than or equal to zero"
}
```

Caso o cliente não tenha saldo suficiente para realizar a transação:

```json
{
  "type": "srn:error:not_enough_funds"
}
```

Caso o cliente tenha passado letras no lugar dos números no valor da recarga, por exemplo.

```json
{
  "type": "srn:error:invalid_params"
}
```
##### **403 - Forbidden**
Caso o cliente não tenha permissão para realizar a recarga.
```json
{
  "type": "srn:error:forbidden"
}
```


<br>

{{< alert title="Status_code: 403" >}}

<br>

Caso receba como resposta o *status_code: 403*, [clique aqui](/docs/referencia-da-api/recargas/fluxo-challenge/) para ter acesso ao *fluxo de autorização do challenge* que deverá ser enviado no *Header* do *Request* (x-stone-challenge-solution). 

{{< /alert >}}


<br>