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
