---
title: "Listar pedidos de portabilidade de salário"
slug: "listar-pedidos-de-portabilidade-de-salário"
hidden: false
createdAt: "2019-09-12T18:42:14.347Z"
updatedAt: "2019-11-25T19:03:57.658Z"
weight: 2
---


```http 
GET https://sandbox-api.openbank.stone.com.br/api/v1/salary_portabilities
```
---

**QUERY PARAMS**

---

**account_id***  `string` 

Formato UUID


---

**status**  `string` 


---

<br>

A portabilidade possui 3 status:
- "CREATED" (Portabilidade foi pedida, porém ainda está sendo processada pela conta de origem)
- "ENABLED" (Portabilidade ativa)
- "DISABLED" (Portabilidade inativa)


---

{{% pageinfo %}}
**Atenção**

Quando uma empresa migra para uma nova Instituição para realizar o pagamento do salário de seus funcionários, o pedido de portabilidade que os funcionários já fizeram na Instituição antiga será perdido. 
Ou seja, caso a empresa opte por trocar de provedor de serviço de Conta Salário, os funcionários terão que fazer novamente o pedido da portabilidade para sua Instituição de preferência.
{{% /pageinfo %}}

---


{{% pageinfo %}}
**Query Param**

É obrigatório passar um query param com o account_id da conta que deseja ver.
{{% /pageinfo %}}

---

{{% pageinfo %}}
**Paginação**

Este endpoint utiliza paginação: [Link](https://docs.openbank.stone.com.br/reference#paginação)
{{% /pageinfo %}}

---


##### **Response**

```JSON
200 ok 
```

```JSON
{
  "cursor": {
    "after": null,
    "before": null,
    "limit": 25
  },
  "data": [
    {
      "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
      "created_at": "2019-08-21T05:32:59Z",
      "created_by": "user:ae8d62c3-4f58-400a-a81d-6abef678a4b3",
      "disabled_at": "2019-08-23T18:29:20Z",
      "employer_document": "81662119000121",
      "employer_name": "chefinho",
      "enabled_at": null,
      "id": "51e761be-9038-4ba4-89e7-d07276b83e3f",
      "payroll_institution_ispb": "00000000",
      "payroll_institution_name": "Banco do Brasil S.A.",
      "payroll_institution_number_code": "001",
      "status": "DISABLED"
    },
    {
      "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
      "created_at": "2019-08-22T15:33:06Z",
      "created_by": "user:ae8d62c3-4f58-400a-a81d-6abef678a4b3",
      "disabled_at": "2019-08-23T21:09:46Z",
      "employer_document": "81662119000121",
      "employer_name": "chefinho",
      "enabled_at": null,
      "id": "9194ce49-65e1-47ae-9262-f0e7fa5ff078",
      "payroll_institution_ispb": "60701190",
      "payroll_institution_name": "Itaú Unibanco  S.A.",
      "payroll_institution_number_code": "341",
      "status": "DISABLED"
    }
  ]
}
```

---

```JSON
400 Bad Request 
```

```JSON
{
  
}
```

---

```JSON
403 Forbbiden 
```

```