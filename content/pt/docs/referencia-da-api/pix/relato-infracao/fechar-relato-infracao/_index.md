---
title: "Fechar Relato de Infração"
linkTitle: "Fechar Relato de Infração"
date: 2022-03-08T15:17:00-03:00
lastmod: 2022-03-08T15:20:00-03:00
weight: 9
description: >
  
---

Através desse endpoint será possível que um participante indireto possa fechar um relato de infração.


```
POST https://sandbox-api.openbank.stone.com.br/api/v1/pix/{{account_id}}/infractions_reports/{{id}}/actions/{{analysis_result}}
<br>
```

##### **HEADERS**
---

**authorization*** `string`
<br> Bearer token de autenticação.

**x-stone-account-id*** `string`
<br> Necessário para permissionamento.

<br>

##### **PATH PARAMS**
---
<br>

**account_id*** `string`
<br>Identificador da conta

**id*** `string`
<br>Identificador do relato

**analysis_result*** `string`
<br>Resultado da análise: aqui deverá ser preenchido o valor accepted ou rejected

##### **BODY PARAMS**
---
<br>
**analysis_details** `string`
<br> Detalhes da análise

**- Para fechar um relato de infração**


```json
{
    "analysis_details": "detalhes da análise"
}

<br> <br> 
```

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
