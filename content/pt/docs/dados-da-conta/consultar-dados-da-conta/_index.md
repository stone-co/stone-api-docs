---
title: "Consultar Dados da Conta"
slug: "consultar-dados-da-conta"
hidden: false
createdAt: "2019-04-01T18:52:27.251Z"
updatedAt: "2019-12-02T22:56:58.116Z"
weight: 3
---

---

```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/accounts/account_id
```
---

**PATH PARAMS**

---

**account_id***  `string` 

Identificador da conta no formato UUID.


{{% pageinfo %}}
**Atenção**


A primeira coisa que faremos antes de lhe dar acesso a dados de uma conta é verificar se você tem acesso a essa conta. Caso você erre o id da conta, sempre receberá o erro de não autorizado.
{{% /pageinfo %}}


---

##### **Response**

```http request
200 ok

{ 
    "account_code": "403881",
    "branch_code": "1",
    "id": "8cbeb3d2-750f-4b14-81a1-143ad715c273",
    "owner_document": "31455351881",
    "owner_id": "user:08807157-f8e1-439e-a2ec-154ecb4bee13",
    "owner_name": "Nome da Usuária",
    "created_at": "2019-07-31T19:13:56Z"
}
```