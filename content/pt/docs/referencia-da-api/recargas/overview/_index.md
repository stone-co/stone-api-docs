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


{{< alert title="Atenção" >}}

Para efetuar uma recarga o cliente precisa ter saldo suficiente em conta, a recarga é cobrada logo após a confirmação.

{{< /alert >}}

<br>

#### **Glossário**
---
<br>

Informações (Chave/Valor) que serão usadas nos fluxos de recargas.

<br>


| Chave                               | Valor                                                               |
| ----------------------------------- | ------------------------------------------------------------------- |
| account_id						  |	Identificador da conta. 											|				
| amount							  |	Valor da recarga desejado.											|
| provider_id						  | Id da operadora. 													|
| client_code 						  | CPF ou Código do assinante do produto. 								|
| product_quota 					  | Informação referente a quota do bilhete único de SP.				|
| product_code 						  | Informação referente ao código do bilhete único de SP.				|
| x-stone-idempotency-key 			  | Valor exclusivo gerado pelo cliente que o servidor de recursos usa para reconhecer novas tentativas subsequentes da mesma solicitação. Para gerar um UUID [clique aqui](https://www.uuidgenerator.net/) (Opcional) |


<br>

#### **Tipos de Recargas**
---

<br>


- [**Recarga de Celular;**](/docs/referencia-da-api/recargas/recarga-de-celular/)

- [**Recarga de Jogos;**](/docs/referencia-da-api/recargas/recarga-de-jogos/)

- [**Conteúdo Digital;**](/docs/referencia-da-api/recargas/recarga-de-conteudo-digital/)

- [**TV por assinatura;**](/docs/referencia-da-api/recargas/recarga-de-tv-por-assinatura/)

- [**Meios de Transporte.**](/docs/referencia-da-api/recargas/recarga-de-meios-de-transporte/)


<br>











