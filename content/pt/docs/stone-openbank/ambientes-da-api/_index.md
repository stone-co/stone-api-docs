---
title: "Ambientes"
linkTitle: "Ambientes"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 2
draft: false
description: >
      
---
<br>
A API pode ser utilizada através de dois ambientes completamente separados: produção e sandbox. 
Usuárias criadas em ambiente de Sandbox não existem em Produção, e vice-versa. As configurações da aplicação também são 100% apartados. 
<br>
{{< alert title="Homologação">}} Após a integração temos uma etapa de homologação das funcionalidades integradas. É preciso ser aprovado na homologação para liberação das chaves de produção. 
{{< /alert >}}


### Ambiente de Sandbox

É destinado à testes e pode ser acessado pelo endpoint:

```http request
https://sandbox-api.openbank.stone.com.br.
```
<br>

### Ambiente de Produção

É onde ocorrem transações em contas reais e pode ser acessado pelo endpoint:
```http request
https://api.openbank.stone.com.br.
```
