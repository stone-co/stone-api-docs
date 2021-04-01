---
title: "Recarga para Celular"
linkTitle: "Recarga para Celular"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-30-17T18:00:00-03:00
weight: 2
draft: false
description: >
---

---
<br>


#### **Ações a serem executadas para recarga de celular**
---

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


<br>


#### **Fluxo da recarga**

1) Para efetuar a recarga de créditos para um celular é necessário que o cliente nos informe o **número de celular** desejado para a recarga. Com esse número, sugerimos a operadora mais provável desejada para a recarga, porém, também permitimos que o cliente escolha a operadora desejada.

2) Após a **escolha da operadora**, o cliente seleciona o valor que deseja recarregar. Os valores oferecidos não são flexíveis e variam de acordo com a operadora.

3) Ao confirmar a recarga, a Celcoin adiciona os créditos junto a operadora.


##### **Operadoras disponíveis**

- Claro;
- Correios;
- Embratel;
- Nextel;
- Oi;
- Tim;
- Vivo;
- Oi Fixo;
- Algar Fixo;
- Claro Fixo;
- Surf Telecom.


<br>

