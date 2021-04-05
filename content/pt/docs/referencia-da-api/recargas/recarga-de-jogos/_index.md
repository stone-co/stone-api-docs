---
title: "Recarga para Jogos"
linkTitle: "Recarga para Jogos"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-30-17T18:00:00-03:00
weight: 3
draft: false
description: >
---

---
<br>

#### **Fluxo da recarga**
---

<br>

1) Para efetuar a recarga de créditos para um jogo é necessário que o cliente selecione e escolha o plano/valor. Os valores oferecidos não são flexíveis e variam de acordo com o provedor.

2) Diferentemente da recarga de celular, após a confirmação da recarga para um jogo, retornamos o **código PIN** ao cliente.

3) Com o código PIN em mãos, **o cliente acessa o site/app do provedor** e resgata os céditos obtidos.

<br>

##### **Provedores disponíveis**
---

- Blizzard;
- GG Credits Free Fire;
- HABBO;
- League of Legends;
- PS Plus;
- PSN Store;
- Rixty;
- STEAM;
- Xbox Live;
- Xbox Live (CSV).


<br>


#### **Ações a serem executadas para recarga de celular**
---

<br>

##### **1) Listar todos os provedores de jogos**

```http
GET /api/v1/topups/games/providers
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
            "name": "GG Credits Free Fire",
            "id": 2151
        },
        {
            "name": "LEVEL UP",
            "id": 2096
        },
        {
            "name": "PSN Store",
            "id": 2147
        },
        {
            "name": "PS Plus",
            "id": 2148
        },
        {
            "name": "Xbox Live Gold",
            "id": 2125
        },
        {
            "name": "Xbox Live (CSV)",
            "id": 2149
        }
    ]
}
```


<br>

##### **2) Listar todos os valores para o provedor**

```http
GET /api/v1/topups/games/values/{provider-id}
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

**- Name: GG Credits Free Fire / id: 2151**

```Json
{
    "product": [
        {
            "value": 3000
        },
        {
            "value": 5000
        },
        {
            "value": 15000
        }
    ]
}
```

**- Name: LEVEL UP / id: 2096**

```Json
{
    "product": [
        {
            "product_name": "LEVELUP 20",
            "value": 2000
        },
        {
            "product_name": "LEVELUP 40",
            "value": 4000
        }
    ]
}
```

**- Name: PSN Store / id: 2147**

```Json
{
    "product": [
        {
            "product_name": "R$ 30,00 - PlayStation Store",
            "value": 3000
        },
        {
            "product_name": "R$ 60,00 - PlayStation Store",
            "value": 6000
        },
        {
            "product_name": "R$ 100,00 - PlayStation Store",
            "value": 10000
        },
        {
            "product_name": "R$ 250,00 - PlayStation Store",
            "value": 25000
        }
    ]
}
```

**- Name: PS Plus / id: 2148**

```Json
{
    "product": [
        {
            "product_name": "R$ 64,90 - PlayStation Plus 3 meses",
            "value": 6490
        },
        {
            "product_name": "R$ 149,90 - PlayStation Plus 12 meses",
            "value": 14990
        }
    ]
}
```

**- Name: Xbox Live Gold / id: 2125**

```Json
{
    "product": [
        {
            "product_name": "R$ 85,99 - Xbox Live 3 meses",
            "value": 8599
        },
        {
            "product_name": "R$ 171,98 - Xbox Live 6 meses",
            "value": 17198
        },
        {
            "product_name": "R$ 199,00 - Xbox Live 12 meses",
            "value": 19900
        }
    ]
}
```

**- Name: Xbox Live (CSV) / id: 2149**

```Json
{
    "product": [
        {
            "product_name": "R$ 5,00 - GC-Xbox LIVE Brazil",
            "value": 500
        },
        {
            "product_name": "R$ 10,00 - GC-Xbox LIVE Brazil",
            "value": 1000
        },
        {
            "product_name": "R$ 15,00 - GC-Xbox LIVE Brazil",
            "value": 1500
        },
        {
            "product_name": "R$ 20,00 - GC-Xbox LIVE Brazil",
            "value": 2000
        },
        {
            "product_name": "R$ 25,00 - GC-Xbox LIVE Brazil",
            "value": 2500
        },
        {
            "product_name": "R$ 40,00 - GC-Xbox LIVE Brazil",
            "value": 4000
        },
        {
            "product_name": "R$ 60,00 - GC-Xbox LIVE Brazil",
            "value": 6000
        },
        {
            "product_name": "R$ 70,00 - GC-Xbox LIVE Brazil",
            "value": 7000
        }
    ]
}
```

<br>

##### **3) Executar uma recarga de jogos**

```http
POST /api/v1/topups/games/dry-run
```


<br>

##### **4) Confirmar uma recarga de jogos**

```http
POST /api/v1/topups/games
```


<br> <br>