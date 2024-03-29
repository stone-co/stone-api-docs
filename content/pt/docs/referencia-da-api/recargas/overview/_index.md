---
title: "Overview"
linkTitle: "Overview"
date: 2021-03-30T18:00:00-03:00
lastmod: 2021-04-06T18:00:00-03:00
weight: 1
draft: false
description: >
---

---
<br>


Objetivo dessa documentação é pontuar as particularidades de cada tipo de recarga oferecida na nossa API.

Para efetuar uma recarga o cliente precisa ter saldo suficiente em conta, a recarga é cobrada logo após a confirmação;

<br>

{{< alert title="Horário de funcionamento" >}}

<br>

A API de Recargas fica disponível todos os dias da semana, 24 horas por dia!

{{< /alert >}}

<br>



#### **Tipos de Recargas**
---

<br>


- [**Recarga para Celular;**](/docs/referencia-da-api/recargas/recarga-de-celular/)

- [**Recarga para Jogos;**](/docs/referencia-da-api/recargas/recarga-de-jogos/)

- [**Recarga para Conteúdo Digital;**](/docs/referencia-da-api/recargas/recarga-de-conteudo-digital/)

- [**Recarga para TV por Assinatura;**](/docs/referencia-da-api/recargas/recarga-de-tv-por-assinatura/)


<br>


#### **Glossário**
---
<br>

Informações (Chave/Valor) que serão usadas nos fluxos de recargas.

<br>


| Chave                               | Valor                                                               |
| ----------------------------------- | ------------------------------------------------------------------- |
| account_id						  |	Identificador da conta.												|				
| amount							  |	Valor da recarga desejado.											|
| provider_id						  | Id da operadora. 													|
| client_code 						  | CPF ou Código do assinante do produto. 								|
| x-stone-idempotency-key 			  | Valor exclusivo gerado pelo cliente que o servidor de recursos usa para reconhecer novas tentativas subsequentes da mesma solicitação. (Opcional) |



<br>








