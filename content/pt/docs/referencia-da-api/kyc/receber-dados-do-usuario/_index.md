---
title: "Receber dados do usuário"
linkTitle: "Receber dados do usuário"
date: 2021-05-1731T11:30:00-03:00
lastmod: 2021-05-1731T11:30:00-03:00
weight: 2
draft: true
---

Nesse endpoint serão solicitados os dados do usuário necessários para realização do envio dos mesmos para início da análise do KYC.


```http request
GET https://sandbox-api.openbank.stone.com.br/api/v1/screens/home/web
```
<br>

#### **HEADERS**
---
<br>

**authorization** `string`
<br>Bearer token de autenticação

<br>

#### **TESTS PARAMS**
---

```json
if (responseCode.code == 200) {
    response = JSON.parse(responseBody)

    user_id = response["user_kyc_requests"]["user_id"]
    pm.environment.set("user_id", user_id)

    birthdate = getAssessmentIDFor("birthdate", response)
    pm.environment.set("birthdate_id", birthdate)

    phone_number = getAssessmentIDFor("phone_number", response)
    pm.environment.set("phone_number_id", phone_number)

    address = getAssessmentIDFor("address", response)
    pm.environment.set("address_id", address)

    document_photo = getAssessmentIDFor("document_photo", response)
    pm.environment.set("document_photo_id", document_photo)

    document_selfies = getAssessmentIDFor("document_selfies", response)
    pm.environment.set("document_selfies_id", document_selfies)

    total_income_range = getAssessmentIDFor("total_income_range", response)
    pm.environment.set("total_income_range_id", total_income_range)
}

function getAssessmentIDFor(type, response) {
    checks = response["user_kyc_requests"]["checks"]
    assessment = checks.filter(function(check) {
        return check["field_type"] == type
    })
    
    return assessment[0]["id"]
}
```

<br>

