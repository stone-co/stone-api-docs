---
title: "Autenticação"
linkTitle: "Autenticação"
date: 2020-05-06T18:05:29-03:00
lastmod: 2020-09-21T18:00:00-03:00
weight: 2
description: >

---

A nossa API é RESTful, e todas suas respostas são em JSON, nos endpoint base, por ambiente:
 
 - *Sandbox*: https://sandbox-api.openbank.stone.com.br
 - *Produção*: https://api.openbank.stone.com.br
 
 
 Seguimos alguns padrões para alguns tipos de dados em toda a nossa API.
 A seguir, juntamos alguns desses padrões para simplificar a vida da desenvolvedora.
 
 #### Realizando Chamadas Autenticadas
 
 A nossa API só aceita chamadas autenticadas, ou seja, chamadas cujo sujeito da ação conseguimos identificar.

Caso ainda não tenha realizado o procedimento para obter seu token de acesso, por favor siga o passo a passo descrito na página **[Autenticação](https://docs.openbank.stone.com.br/docs/autenticacao-guides)** de nossos Guias.

Caso tenha em mãos seu token de acesso, já é possível realizar chamadas autenticadas.

Para isso, exigimos que nas [requisições HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) exista no cabeçalho um campo chamado `authorization`, cujo valor será \"Bearer\" seguido do token de acesso.

Exemplo de cabeçalho de uma chamada autenticada:

```http request
GET /api/v1/accounts HTTP/1.1
Host: sandbox-api.openbank.stone.com.br
User-Agent: Nome da aplicação
Accept: */*
authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV*adQssw5c
```

{{< alert title="Autenticação nos Exemplos" >}}
Cada exemplo de endpoint desta documentação tem um campo especial para o ACCESS_TOKEN, acessível clicando no botão `Try It`.
{{< /alert >}}
