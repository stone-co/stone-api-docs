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
 
