---
title: "Fechar Relato de Infração"
linkTitle: "Fechar Relato de Infração"
date: 2022-03-08T15:17:00-03:00
lastmod: 2022-03-08T15:20:00-03:00
weight: 9
description: >
  
---
<br>

Através do seguinte endpoint, será possível que um participante indireto feche um relato de infração. Para fechar um relato, este deve possuir os seguintes requisitos: ser um relato recebido (direction: inbound) e estar pendente (status: pending). O relato também deve ser fechado em um prazo de 7 dias.


```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{account_id}}/infractions_reports/{{id}}/actions/{{analysis_result}}

```

<br>

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **PATH PARAMS**
---

**account_id*** `string`
<br>Identificador da conta

**id*** `string`
<br>Identificador do relato

**analysis_result*** `string`
<br>Resultado da análise: aqui deverá ser preenchido com um dos valores `accepted` ou `rejected`

<br>

##### **BODY PARAMS**
---

**analysis_details** `string` `Opcional` `Tamanho máximo de 2000 caracteres`
<br> Detalhes da análise

<br>

##### **Request body**


```json
{
    "analysis_details": "detalhes da análise"
}

```
<br> <br> 

##### **Response**
---

```
204 OK
```

<br>

```
400 Bad Request
```

```json
{
    "reason": [{"error": "is invalid", "path": ["account_id"]}],
    "type": "srn:error:validation"
}
```

<br>

```
403 Forbidden
```

```json
{
    "type": "srn:error:unauthorized"
}
```
