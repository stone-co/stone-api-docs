---
title: "Overview"
linkTitle: "Overview"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-30-17T18:00:00-03:00
weight: 1
draft: false
description: >
---

---

<Inserir aqui um overview de Recargas>


<br> <br> <br>


### **Tipos de Recargas**
---

<br>



#### **Recarga de Celular**

<br>

##### **Listar todos os valores para o provedor**

```http
GET /api/v1/topups/mobile/values/{provider-id}/{cellphone}
```


##### **Listar todos os provedores para celular**

```http
GET /api/v1/topups/mobile/providers/{cellphone}
```


##### **Executar uma recarga de celular**

```http
POST /api/v1/topups/mobile/dry-run
```


##### **Confirmar uma recarga de celular**

```http
POST /api/v1/topups/mobile
```


<br> <br>



#### **Recarga de Jogos**

<br>

##### **Listar todos os valores para o provedor**

```http
GET /api/v1/topups/games/values/{provider-id}
```


##### **Listar todos os provedores de jogos**

```http
GET /api/v1/topups/games/providers
```


##### **Executar uma recarga de jogos**

```http
POST /api/v1/topups/games/dry-run
```


##### **Confirmar uma recarga de jogos**

```http
POST /api/v1/topups/games
```


<br> <br>



#### **Conteúdo Digital**

<br>

##### **Listar todos os valores para o provedor**

```http
GET /api/v1/topups/digital-content/values/{provider-id}
```


##### **Listar todos os provedores de conteúdo digital**

```http
GET /api/v1/topups/digital-content/providers
```


##### **Executar uma recarga de conteúdo digital**

```http
POST /api/v1/topups/digital-content/dry-run
```


##### **Confirme uma recarga de conteúdo digital**

```http
POST /api/v1/topups/digital-content
```


<br> <br>



#### **TV por assinatura**


<br>

##### **Listar todos os valores para o provedor**

```http
GET /api/v1/topups/tv/values/{provider-id}
```


##### **Listar todos os provedores para a TV**

```http
GET /api/v1/topups/tv/providers
```


##### **Executar uma recarga para a TV**

```http
POST /api/v1/topups/tv/dry-run
```


##### **Confirme uma recarga para a TV**

```http
POST /api/v1/topups/tv
```


<br> <br>



#### **Meios de Transporte**

<br>

##### **Listar todos os valores para o provedor**

```http
GET /api/v1/topups/transport/values/{provider-id}
```


##### **Listar todos os provedores para meios de Transporte**

```http
GET /api/v1/topups/transport/providers
```


##### **Executar uma recarga para meios de Transporte**

```http
POST /api/v1/topups/transport/dry-run
```


##### **Confirme uma recarga para a TV**

```http
POST /api/v1/topups/transport
```


<br>


