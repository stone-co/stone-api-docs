---
title: "Calendário de Agendamento"
linkTitle: "Calendário de Agendamento"
slug: "calendário-de-agendamento"
draft: false
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
description: >
---
Lista de feriados e fins de semana presentes em um intervalo de tempo especificado pelos query string params `start` e `end`. O valor default para o parâmetro `start` é o dia atual e o valor default para o parâmetro `end` é o dia atual + 1 ano.

A flag `is_holiday` é `true` quando o dia não útil é um feriado e é `false` quando é apenas um final de semana. Apenas feriados apresentam os campos prefixados por `holiday_` preenchidos.

Cada operação na API (payment, external_transfer e internal_transfer) tem um calendário específico. Por isso, os recursos da API de calendário podem ser acessados indicando sobre qual operação se deseja ter informações do calendário. Isso é feito pelo query string param `operation_type`, que pode assumir os valores: `external_transfer`, `internal_transfer` ou `payment.`

O campo `execution_limit_date` representa o limite para o qual um agendamento pode ser efetuado. O default é dia atual + 1 ano.

O campo `next_available_execution_date` representa o próximo dia disponível para agendamento.

```http
GET https://sandbox-api.openbank.stone.com.br/api/v1/schedulings/calendar
```

---

#### **QUERY PARAMS**

---

**start** `string`
<br>Data que define o início do intervalo no qual serão buscados dias não úteis.
<br>Format: `yyyy-mm-dd`

**end** `string`
<br>Data que define o fim do intervalo no qual serão buscados dias não úteis.
<br>Format: `yyyy-mm-dd`

**operation_type*** `string`
<br>Define qual é a operação relativa ao calendário desejado.
<br>Format: `binary`
<br>Allowed Values: `payment`, `external_tranfer` e `internal_transfer`

<br>

---

#### **HEADERS**

---

**If-None-Match** `string`
<br>Etag. Se for igual etag do conteúdo, a resposta será 304

<br>
<br>

---

#### **Response**

---

```JSON
201 Created
content-type: application/json
```
Body

```JSON
        {
            "execution_limit_date": "2020-03-30",
            "next_available_execution_date": "2019-04-01",
            "non_business_days": [
                {
                "date": "2019-03-30",
                "is_weekend": true,
                "is_holiday": true,
                "holiday_description": "Feriado"
                },
                {
                "date": "2019-03-31",
                "is_weekend": true,
                "is_holiday": false,
                "holiday_description": null
                }
            ]
        }
```
