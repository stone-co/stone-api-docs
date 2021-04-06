---
title: "Recarga para TV por Assinatura"
linkTitle: "Recarga para TV por Assinatura"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-30-17T18:00:00-03:00
weight: 5
draft: false
description: >
---

---
<br>

#### **Fluxo da recarga**
---

<br>


1) Para efetuar a recarga de créditos para uma Tv por Assinatura é necessário que o cliente nos informe o **CPF** ou **Código do Assinante** e escolha o **provedor**. 

2) Após a confirmação, a Celcoin adiciona os créditos junto ao provedor.


<br>


##### **Provedores disponíveis**
---

<br>

- Claro TV;
- Oi TV;
- SKY TV.

{{< alert title="Atenção" >}}

<br>

Para cada provedor, há um diferente **plano/valor** disponível.

{{< /alert >}}


<br>


#### **Ações a serem executadas para recarga de TV por Assinatura**
---

<br>



##### **1) Listar todos os provedores para a TV**

```http
GET /api/v1/topups/tv/providers
```

###### **Header request**

```Json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

###### **Response**

```Json
200 ok
```

```Json
{
    "providers": [
        {
            "name": "Claro TV",
            "id": 2126
        },
        {
            "name": "Oi TV",
            "id": 2140
        },
        {
            "name": "SKY TV",
            "id": 2127
        }
    ]
}
```


<br>

##### **2) Listar todos os valores para o provedor**

```http
GET /api/v1/topups/tv/values/{provider-id}
```

###### **Header request**

```Json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

###### **Responses**

```Json
200 ok
```

**- Name: Claro TV / id: 2126**

```Json
{
    "product": [
        {
            "product_name": "R$ 18,00 - INICIAL 30d",
            "value": 1800
        },
        {
            "product_name": "R$ 36,00 - LIGHT 15d",
            "value": 3600
        },
        {
            "product_name": "R$ 55,00 - MIX 15d",
            "value": 5500
        },
        {
            "product_name": "R$ 58,00 - LIGHT 30d",
            "value": 5800
        },
        {
            "product_name": "R$ 80,00 - TOP 15d",
            "value": 8000
        },
        {
            "product_name": "R$ 86,00 - MIX 30d",
            "value": 8600
        },
        {
            "product_name": "R$ 109,00 - TOP 30d",
            "value": 10900
        }
    ]
}
```

**- Name: Oi TV / id: 2140**

```Json
{
    "product": [
        {
            "product_name": "START HD-15D R$ 44,90",
            "value": 4490
        },
        {
            "product_name": "MIX HD-15D R$ 59,90",
            "value": 5990
        },
        {
            "product_name": "START HD-30D R$ 69,90",
            "value": 6990
        },
        {
            "product_name": "MIX HD-30DR$ 94,90",
            "value": 9490
        }
    ]
}
```

**- Name: SKY TV / id: 2127**

```Json
{
    "product": [
        {
            "product_name": "R$ 11,90 REC SMART - 3 DI",
            "value": 1190
        },
        {
            "product_name": "R$ 18,90 REC DIGITAL - 30",
            "value": 1889
        },
        {
            "product_name": "R$ 19,90 REC SMART - 7 DI",
            "value": 1989
        },
        {
            "product_name": "R$ 21,90 REC SMART3D + TL",
            "value": 2190
        },
        {
            "product_name": "R$ 33,90 REC NEW MASTER -",
            "value": 3390
        },
        {
            "product_name": "R$ 35,90 REC NEW MASTER 0",
            "value": 3590
        },
        {
            "product_name": "R$ 36,90 REC SMART - 15 D",
            "value": 3690
        },
        {
            "product_name": "R$ 44,90 REC SMART7D+ FUT",
            "value": 4490
        },
        {
            "product_name": "R$ 48,90 REC NEW MASTER 0",
            "value": 4890
        },
        {
            "product_name": "R$ 52,90 REC SMART 7D + C",
            "value": 5290
        },
        {
            "product_name": "R$ 55,90 REC NEW MASTER -",
            "value": 5590
        },
        {
            "product_name": "R$ 57,90 REC SMART15D+TLC",
            "value": 5790
        },
        {
            "product_name": "R$ 58,90 REC NEW MASTER 0",
            "value": 5890
        },
        {
            "product_name": "R$ 65,90 REC NEW MASTER 7",
            "value": 6590
        },
        {
            "product_name": "R$ 69,90 REC SMART15D+ FU",
            "value": 6990
        },
        {
            "product_name": "R$ 81,90 REC SMART 30D + ",
            "value": 8190
        },
        {
            "product_name": "R$ 84,90 REC SMART 30D + ",
            "value": 8490
        },
        {
            "product_name": "R$ 86,90 REC NEW MASTER- ",
            "value": 8690
        },
        {
            "product_name": "R$ 96,90 REC SMART30D+ FU",
            "value": 9690
        },
        {
            "product_name": "R$ 98,90 REC SMART - 60 D",
            "value": 9890
        },
        {
            "product_name": "R$ 142,80 REC DIGITAL 12 M",
            "value": 14280
        }
    ]
}
```


<br>

##### **3) Executar uma recarga para a TV**

```http
POST /api/v1/topups/tv/dry-run
```

###### **Header request**

```Json
{
	"authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4d3NUd3BhYTRJWUZIYWV5ZFRubnRoRC1UaVlCaU9kanNmOGx6RUlMR1hVIn0.eyJqdGkiOiJiODQ0NDc4OS01ODE5LTQ4MTUtYjc1NC04MDU5NmMyYTg4MGYiLCJleHAiOjE2MTY2OTk5MjQsIm5iZiI6MCwiaWF0IjoxNjE2Njk5MDI0LCJpc3MiOiJodHRwczovL3NhbmRib3gtYWNjb3VudHMub3BlbmJhbmsuc3RvbmUuY29tLmJyL2F1dGgvcmVhbG1zL3N0b25lX2JhbmsiLCJzdWIiOiJhYzE5MGRmYy00YTBjLTQ5ODUtYmQwNi03NWE5Zjc3NjU0MTMiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiIwNjVlY2IwOC0yNDM5LTQwYzAtOGUxMy0yYjQzYzIxNzQzZTMiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiIwMjhlMjY3ZS0zMjYwLTQzNDMtODQ2ZS1hOTRkNzlmZTFjYWEiLCJhY3IiOiIxIiwic2NvcGUiOiJwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6d3JpdGUgcGF5bWVudGFjY291bnQ6Y29udGFjdDp3cml0ZSBlbnRpdHk6d3JpdGUgcGF5bWVudGFjY291bnQ6cmVhZCBwYXltZW50YWNjb3VudDp0cmFuc2ZlcnM6aW50ZXJuYWwgcGF5bWVudGFjY291bnQ6ZmVlczpyZWFkIHBheW1lbnRhY2NvdW50Omluc3RhbnRwYXltZW50IHBheW1lbnRhY2NvdW50OnBheW1lbnRzIHN0b25lX3N1YmplY3RfaWQgcGF5bWVudGFjY291bnQ6Y29udGFjdDpyZWFkIHNpZ251cDpwYXltZW50YWNjb3VudCBwYXltZW50YWNjb3VudDpib2xldG9pc3N1YW5jZSBwYXltZW50YWNjb3VudDpwYXltZW50bGlua3M6cmVhZCBwYXltZW50YWNjb3VudDpwYXlyb2xsczpyZWFkIHBheW1lbnRhY2NvdW50OnBheXJvbGxzOndyaXRlIHBheW1lbnRhY2NvdW50OnRyYW5zZmVyczpleHRlcm5hbCBlbnRpdHk6cmVhZCIsImNsaWVudElkIjoiMDY1ZWNiMDgtMjQzOS00MGMwLThlMTMtMmI0M2MyMTc0M2UzIiwiY2xpZW50SG9zdCI6IjEwLjEwLjEuMTQ5Iiwic3RvbmVfc3ViamVjdF9pZCI6ImFwcGxpY2F0aW9uOjA2NWVjYjA4LTI0MzktNDBjMC04ZTEzLTJiNDNjMjE3NDNlMyIsImNsaWVudEFkZHJlc3MiOiIxMC4xMC4xLjE0OSJ9.PlAhWLgC2W10H9emucF4obcJhwR92EogMNRIWUej4z-P-p3UaStYlaYd5Bfx4hl7da4ly62K1LEBI7LOqCFkbHMlnJfglp3dFS2M3iHZ571BNSmCff3wUiFy6zoHxFaKEUPy0V8e6mCQwFuapdIvDocA4Z4xYh049dWEwbJ2uevV3V_Q-RL3me8vykNTWGiT-dmyWvFN-XAq889_F1ZQskHsLz-ZtlrFw3XjitnLvEJbg9iyxVA7AuwnexBIQS4gU9QwMXcJjij9JowYbLu4ANUITXU01Jf5hxMYq1oSobOL3-RuGWJLoPOXkJyAbOm5hS15QgSuwp_qOU8VAEa3Yg"
}
```

###### **Body Request**

```Json
{
  "account_id": "e4043bb5-542b-46f6-bcbc-0e63d37e1c47",
  "amount": 0,
  "client_code": "10036389709",
  "provider_id": "2126"
}
```

###### **Response**

```Json
202 Accepted
```

```Json
{
    "amount": 10900,
    "account_id": "e4043bb5-542b-46f6-bcbc-0e63d37e1c47",
    "provider_id": "2126",
    "client_code": "10036389709"
}
```


<br>



##### **4) Confirme uma recarga para a TV**

```http
POST /api/v1/topups/tv
```


<br> <br>