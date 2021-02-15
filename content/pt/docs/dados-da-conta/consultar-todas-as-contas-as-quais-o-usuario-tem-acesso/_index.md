---
title: "Consultar Todas Contas às Quais Se Tem Acesso"
slug: "consultar-todas-contas-às-quais-a-usuária-tem-acesso"
hidden: false
createdAt: "2019-04-01T19:11:50.634Z"
updatedAt: "2020-04-30T00:51:36.790Z"
weight: 4

---

---

```http 
GET https://sandbox-api.openbank.stone.com.br/api/accounts
```
---

**QUERY PARAMS**

---

**paginate***  `boolean`

{{% pageinfo %}}
**Atenção**

Caso 'true', irá limitar a mostrar somente 50 contas, se for setado para 'false' mostrará todas as contas as quais o usuário tem acesso.
 
{{% /pageinfo %}}



---

##### **Response**

```JSON
200 OK
content-type: application/json
```
Body
```JSON
{
    "cursor": {
        "after": null,
        "before": null,
        "limit": 50
    },
    "data": [
        {
            "account_code": "403881",
            "branch_code": "1",
            "id": "31091cb9-26e1-407c-a363-3578f6f28289",
            "owner_document": "96156305270",
            "owner_id": "user:23f7eb28-5ab3-4606-8b59-55e9d89f02bd",
            "owner_name": "Nome da Usuária",
          	"created_at": "2019-07-31T19:13:56Z"
        }
    ]
}
```