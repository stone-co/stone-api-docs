---
title: "Criar pedido de portabilidade de salário"
slug: "criar-pedido-de-portabilidade"
excerpt: "Cria um pedido de portabilidade de salário para uma conta"
hidden: false
date: "2019-09-12T18:35:00.384Z"
lastmod: "2019-12-03T21:12:58.641Z"
weight: 1
description: >
---

 Cria um pedido de portabilidade de salário para uma conta.

---


``` 
POST https://sandbox-api.openbank.stone.com.br/api/v1/salary_portabilities
```
---

#### **BODY PARAMS**

---

**account_id***  `string` 

Identificador da conta no formato UUID.


---

**employer_document***  `string` 

CNPJ


---

**employer_name**  `string` 


---

**payroll_institution_code***  `string` 

ISPB ou código da instituição.


<br>

---

#### **Response**

```
201 Created 
```
Body
```json
{
  "id": "51e761be-9038-4ba4-89e7-d07276b83e3f",
  "created_by": "user:51e761be-9038-4ba4-89e7-d07276b83e3f",
  "created_at": "2018-08-14T14:45:53Z",
  "enabled_at": "2018-09-14T14:45:53Z",
  "disabled_at": null,
  "status": "ENABLED",
  "account_id": "477f8576-ca82-462b-be73-dc28cc6490c3",
  "employer_document": "81662119000121",
  "employer_name": "Some employer",
  "payroll_institution_ispb": "00000000",
  "payroll_institution_number_code": "001",
  "payroll_institution_name": "Banco do Brasil"
}
```

---

```
400 Bad Request 
```

```json
{
    "reason": [
        {
            "error": "can't be blank",
            "path": [
                "payroll_institution_code"
            ]
        },
        {
            "error": "can't be blank",
            "path": [
                "employer_document"
            ]
        },
        {
            "error": "can't be blank",
            "path": [
                "account_id"
            ]
        }
    ],
    "type": "srn:error:validation"
}
```

---


```
403 Forbidden 
```

```json
{
    "challenge": null,
    "details": {
        "error": "client_unauthorized"
    },
    "id": "477f8576-ca82-462b-be73-dc28cc6490c3",
    "type": "srn:error:client_unauthorized"
}
```
