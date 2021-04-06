---
title: "Recarga para Meios de Transporte"
linkTitle: "Recarga para Meios de Transporte"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-30-17T18:00:00-03:00
weight: 6
draft: false
description: >
---

---
<br>

#### **Fluxo da recarga**
---

<br>

O Fluxo de recarga se diferencia para os dois Provedores disponíveis:

<br>

- Uber

1) Para efetuar a recarga de créditos para o Provedor Uber é necessário que o cliente selecione e escolha o plano/valor.  

2) Após a confirmação da recarga para o Provedor Uber, retornamos o **código PIN** ao cliente.

3) Com o código PIN em mãos, **o cliente acessa o site/app do provedor** e resgata os céditos obtidos.

<br>

- Bilhete Único de SP


1) Para efetuar a recarga de créditos para o Provedor Bilhete Único SP é necessário que o cliente informe o número do bilhete único.  

2) É necessário que o cliente informe o tipo de recarga (Comun / Diário / Mensal).

3) Por fim, informar o valor da recarga.



<br>


##### **Provedores disponíveis**
---

<br>

- Uber;
- Bilhete Único de SP.

{{< alert title="Atenção" >}}

<br>

O valor escolhido para recarga do Provedor Uber, deverá estar entre R$1,00 e R$121,00.

O valor de recarga para o provedor Bilhete Único de SP varia de acordo com as quotas mínimas/máximas pré-estabelecidas. 

{{< /alert >}}


<br>


#### **Ações a serem executadas para recarga de Meios de Transporte**
---





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


