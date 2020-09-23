---
title: "Autenticação"
linkTitle: "Autenticação"
date: 2020-05-06T18:05:29-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 2
description: >

---

 
A nossa API só aceita chamadas autenticadas, ou seja, chamadas cujo sujeito da ação conseguimos identificar. Para isso, exigimos que nas [requisições HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) exista no cabeçalho um campo chamado `authorization`, cujo valor será \"Bearer\" seguido do `access_token`.

Exemplo de cabeçalho de uma chamada autenticada:

```http request
GET /api/v1/accounts HTTP/1.1
Host: sandbox-api.openbank.stone.com.br
User-Agent: Nome da aplicação
Accept: */*
authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV*adQssw5c
```
