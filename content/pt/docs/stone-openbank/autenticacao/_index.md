---
title: "Autenticação"
slug: "autenticação-1"
hidden: false
weight: 2
draft: false
createdAt: "2019-07-23T18:56:58.292Z"
updatedAt: "2020-05-13T16:47:34.859Z"
---
A nossa API é RESTful, e todas suas respostas são em JSON, nos endpoint base, por ambiente:

- _Sandbox_: https://sandbox-api.openbank.stone.com.br
- _Produção_: https://api.openbank.stone.com.br


Seguimos alguns padrões para alguns tipos de dados em toda a nossa API.
A seguir, juntamos alguns desses padrões para simplificar a vida da desenvolvedora.


### Realizando Chamadas Autenticadas


A nossa API só aceita chamadas autenticadas, ou seja, chamadas cujo sujeito da ação conseguimos identificar.

Caso ainda não tenha realizado o procedimento para obter seu token de acesso, por favor siga o passo a passo descrito na página **[Autenticação](/docs/guias/integracao/autenticacao/)** de nossos Guias.

Caso tenha em mãos seu token de acesso, já é possível realizar chamadas autenticadas.

Para isso, exigimos que nas [requisições HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) exista no cabeçalho um campo chamado `authorization`, cujo valor será "Bearer" seguido do token de acesso.

Exemplo de cabeçalho de uma chamada autenticada:


##### **Header**

```text
GET /api/v1/accounts HTTP/1.1
Host: sandbox-api.openbank.stone.com.br
User-Agent: Nome da aplicação
Accept: */*
authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
