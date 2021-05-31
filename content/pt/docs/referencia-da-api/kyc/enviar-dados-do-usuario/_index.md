---
title: "Enviar dados do usuário"
linkTitle: "Enviar dados do usuário"
date: 2021-05-1731T11:30:00-03:00
lastmod: 2021-05-1731T11:30:00-03:00
weight: 4
---

Nesse endpoint serão solicitados os dados do usuário necessários para realização do envio dos mesmos para início da análise do KYC.


```http request
POST https://sandbox-api.openbank.stone.com.br/api/v1/users/{{user_id}}/kyc/answer
```
<br>

#### **HEADERS**
---
<br>

**authorization** `string`
<br>Bearer token de autenticação

<br>

#### **PATH PARAMS**
---

<br>

**user_id*** `string`
Identificador do usuário recebido no response da chamada da API para Criar novos pedidos de usuários.
Ex: ef49c647-1dc9-58e8-a559-108cdf7e65a4

<br>

#### **BODY PARAMS**
---

```json
{
    "answers": [
        {
            "check_id": "{{birthdate_id}}",
            "value": "2000-10-10"
        },
        {
            "check_id": "{{phone_number_id}}",
            "value": "21971697123"
        },
        {
            "check_id": "{{address_id}}",
            "value": {
                "street": "Rua Buarque de Macedo",
                "city": "Rio de Janeiro",
                "country": "Brasil",
                "extra": "",
                "postal_code": "22220030",
                "street_number": "38383838",
                "neighborhood": "Flamengo",
                "state": "RJ",
                "reference_point": ""
            }
        },
        {
            "check_id": "{{document_photo_id}}",
            "value": {
                "type": "CNH",
                "front": "https://storage.googleapis.com/sdb-inside-gateway-frontend-3727/dXNlcjo4YTZmMzYzZi05Mzg4LTRiMzEtOGY0ZC05Zjk2NTAyY2Q1NzA=/53acaa13-f74b-4884-9420-f05b0ca79d25/doc_cnh_front.jpg",
                "back": "https://storage.googleapis.com/sdb-inside-gateway-frontend-3727/dXNlcjo4YTZmMzYzZi05Mzg4LTRiMzEtOGY0ZC05Zjk2NTAyY2Q1NzA=/53acaa13-f74b-4884-9420-f05b0ca79d25/doc_cnh_front.jpg"
            }
        },
        {
            "check_id": "{{document_selfies_id}}",
            "value": [
                "https:\/\/storage.googleapis.com\/hml-inside-gateway-frontend-4715\/dXNlcjplZDFhZTdjYy0zZGRhLTQ3MGMtYjlhMi02ZmI5MzJhY2U2NDc=\/79767818-0254-4f85-9cdb-f560013036d0\/CBED44AF-900B-4EC7-B8BF-DB7373BF4070.jpg",
                "https:\/\/storage.googleapis.com\/hml-inside-gateway-frontend-4715\/dXNlcjplZDFhZTdjYy0zZGRhLTQ3MGMtYjlhMi02ZmI5MzJhY2U2NDc=\/b2ea2032-c7f2-4c4d-b377-90920afec4cd\/43964A19-69C4-451B-8CF9-B66F8C8CC0A8.jpg",
                "https:\/\/storage.googleapis.com\/hml-inside-gateway-frontend-4715\/dXNlcjplZDFhZTdjYy0zZGRhLTQ3MGMtYjlhMi02ZmI5MzJhY2U2NDc=\/6aacb6d4-91f2-416e-8b04-72cca5313984\/591B208A-0374-4642-A38E-DAC0A9AFCF53.jpg",
                "https:\/\/storage.googleapis.com\/hml-inside-gateway-frontend-4715\/dXNlcjplZDFhZTdjYy0zZGRhLTQ3MGMtYjlhMi02ZmI5MzJhY2U2NDc=\/43e42571-4d6e-4fda-9b45-c99276b18024\/B6076B95-B67F-4DAE-85F1-CAB1FA013B30.jpg",
                "https:\/\/storage.googleapis.com\/hml-inside-gateway-frontend-4715\/dXNlcjplZDFhZTdjYy0zZGRhLTQ3MGMtYjlhMi02ZmI5MzJhY2U2NDc=\/89f45dbc-5797-4f4c-b067-8d04e7dc1c6d\/7BFB3285-BE78-4F73-B36E-087DDD82CA6A.jpg",
                "https:\/\/storage.googleapis.com\/hml-inside-gateway-frontend-4715\/dXNlcjplZDFhZTdjYy0zZGRhLTQ3MGMtYjlhMi02ZmI5MzJhY2U2NDc=\/acddcea6-94ce-4d70-bf8a-95f8b1cfa145\/8673814D-7B81-4DEB-A15A-CD431A91DAD2.jpg"
            ]
        },
        {
            "check_id": "{{total_income_range_id}}",
            "value": {
                "upper_bounds": 500000
            }
        }
    ]
}
```

<br>

#### **Response**
---

```http
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
            "status": "answered",
            "updated_at": "2021-05-31T20:10:18Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "phone_number",
            "id": "6747569e-ea50-4b71-9230-7e0fd8b92d6d",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "answered",
            "updated_at": "2021-05-31T20:10:18Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "address",
            "id": "4f485886-1546-4726-b4e1-baa21bb0f4a1",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "answered",
            "updated_at": "2021-05-31T20:10:18Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "document_photo",
            "id": "cbe5a713-2d02-49b3-85e4-97bf39c27354",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "answered",
            "updated_at": "2021-05-31T20:10:18Z"
        },
        {
            "context": null,
            "created_at": "2021-05-31T15:04:48Z",
            "detailed_reason": "Precisamos de algumas informações",
            "field_type": "document_selfies",
            "id": "5b6d185d-e080-4534-b346-389fffae7294",
            "input_type": "user_input",
            "reason": "account_request",
            "status": "answered",
            "updated_at": "2021-05-31T20:10:18Z"
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
            "status": "answered",
            "updated_at": "2021-05-31T20:10:18Z"
        }
    ],
    "context": {},
    "created_at": "2021-05-31T15:04:48Z",
    "id": "50a22e82-1fe6-407b-b76c-986f46db60e8",
    "input_type": "user_input",
    "is_mandatory": true,
    "reason": "account_request",
    "status": "answered",
    "updated_at": "2021-05-31T20:10:18Z",
    "user_id": "ef49c647-1dc9-47e8-a559-108cdf7e65a4"
}
```