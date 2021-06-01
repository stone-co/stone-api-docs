---
title: "Buscar informações pendentes"
linkTitle: "Buscar informações pendentes"
date: 2021-05-1731T11:30:00-03:00
lastmod: 2021-05-1731T11:30:00-03:00
weight: 1
---
---

<br>

Nesse endpoint é possível verificar as informações de KYC que se encontram pendentes de resposta.

A partir do _response_ desse endpoint, é possível verificar os _ids_ das informações que estão faltando para que possamos enviar os dados no endpoint para [responder o KYC](/docs/referencia-da-api/kyc/enviar-dados-do-usuario/).

<br>

```http request
GET https://sandbox-api.openbank.stone.com.br/api/v1/users/{id_do_usuario}/kyc/request
```
<br>

#### **HEADERS**
---
<br>

**authorization** `string`
<br>Bearer token de autenticação

<br>

#### **Response**
---

```Json
200 OK
```

```json
{
    "checks": [
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "birthdate",
            "id": "400bf541-788f-4d5f-86b1-6519f318ca65",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "requested",
            "updated_at": "2021-05-31T15:04:48Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "phone_number",
            "id": "6747569e-ea50-4b71-9230-7e0fd8b92d6d",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "requested",
            "updated_at": "2021-05-31T15:04:48Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "address",
            "id": "4f485886-1546-4726-b4e1-baa21bb0f4a1",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "requested",
            "updated_at": "2021-05-31T15:04:48Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "document_photo",
            "id": "cbe5a713-2d02-49b3-85e4-97bf39c27354",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "requested",
            "updated_at": "2021-05-31T15:04:48Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "document_selfies",
            "id": "5b6d185d-e080-4534-b346-389fffae7294",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "requested",
            "updated_at": "2021-05-31T15:04:48Z"
        },
        {
            "context": {
                "income_ranges": [
                    {
                        "formatted": "Até R$ 5.000,00",
                        "range": {
                            "lower_bounds": null,
                            "upper_bounds": 500000
                        }
                    },
                    {
                        "formatted": "Entre R$ 5.000,01 e R$ 10.000,00",
                        "range": {
                            "lower_bounds": 500001,
                            "upper_bounds": 1000000
                        }
                    },
                    {
                        "formatted": "Entre R$ 10.000,01 e R$ 20.000,00",
                        "range": {
                            "lower_bounds": 1000001,
                            "upper_bounds": 2000000
                        }
                    },
                    {
                        "formatted": "Entre R$ 20.000,01 e R$ 100.000,00",
                        "range": {
                            "lower_bounds": 2000001,
                            "upper_bounds": 10000000
                        }
                    },
                    {
                        "formatted": "Entre R$ 100.000,01 e R$ 1.000.000,00",
                        "range": {
                            "lower_bounds": 10000001,
                            "upper_bounds": 100000000
                        }
                    },
                    {
                        "formatted": "Mais de R$ 1.000.000,00",
                        "range": {
                            "lower_bounds": 100000001,
                            "upper_bounds": null
                        }
                    }
                ]
            },
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "total_income_range",
            "id": "a24ad007-2d63-4108-8340-16b843873be2",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "requested",
            "updated_at": "2021-05-31T15:04:48Z"
        }
    ],
    "context": {},
    "created_at": "2021-05-31T15:04:48Z",
    "id": "50a22e82-1fe6-407b-b76c-986f46db60e8",
    "input_type": "user_input",
    "is_mandatory": true,
    "reason": "account_request",
    "status": "requested",
    "updated_at": "2021-05-31T15:04:48Z",
    "user_id": "ef49c647-1dc9-47e8-a559-108cdf7e65a4"
}
```
<br>

Próximo passo:

#### [Consultar URL para envio da foto](/docs/referencia-da-api/kyc/consultar-url-para-foto/).
