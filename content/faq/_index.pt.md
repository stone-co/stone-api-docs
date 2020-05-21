---
title: "FAQ"
date: 2020-04-27T21:29:14-03:00
lastmod: 2020-04-27T21:30:41-03:00
draft: false
icon: "ti-help"
description: "Tire suas dúvidas aqui!"
type : "docs"
weight: "5"
---

{{< faq "Qual a diferença entre o status *failed* e *refunded*?" >}}
*Refunded* é o status correspondente a uma devolução. Ou seja, chegamos a efetuar a operação e enviá-la para a instituição de destino e a mesma foi devolvida. As operações que podem sofrer devolução são transferências externas e pagamentos. É possivel ver no extrato tanto a operação criada, quando sua devolução. 
*Failed* é o status correspondente a uma falha. Ou seja, na hora de processarmos a operação internamente tivemos alguma falha. As operações que podem sofrer uma falha são: transferências externas, transferências internas e pagamentos. Essas operações não podem ser vistas no extrato porque não chegaram a de fato gerar uma movimentação. 
{{</ faq >}}

{{< faq "Quando a taxa é devolvida de uma transação *refunded*? E no caso de uma transação *failed*?" >}}
Quando a transação passa para o status *refunded* a taxa referente aquela movimentação é devolvida imeditamente para a conta. No caso de uma transação que falha no processamento a taxa nem chega a ser cobrada da usuária. 
{{</ faq >}}

{{< faq "A partir de que momento é possível pedir *consent* para uma conta?" >}}
O consentimento é dado por um sujeito (usuária, a uma aplicação, sobre um determinado recurso (conta pagamento). Assim só é possível que o consentimento seja dado após a abertura da conta. Além disso, pelo consentimento ser um fluxo logado é preciso que a usuária tenha ao menos criado sua senha de acesso. 
{{</ faq >}}

{{< faq "Em quanto tempo uma TED chega a conta de destino?" >}}
Isso depende diretamente do tempo de processamento da instituição de destido, sendo assim não é possível identificar o momento exato que a TED entra na outra conta. Mas, apesar de assíncrono, é possível acompanhar pelos webhooks o momento que iniciamos o processamento interno (cash_out_external_transfer_execution_started) e que finalizamos o envio (cash_out_external_transfer_finished) para a outra instituição. 
{{</ faq >}}

{{< faq "Para que instituições é possível fazer TEDs?" >}}
É possível fazer TEDs para todas as intituições participantes Sistema de Transferência de Reservas (STR) do Sitema de Pagamentos Brasileiro (SPB). Você pode ver a lista completa dos participantes do STR no site do [Banco Central](https://dadosabertos.bcb.gov.br/dataset/lista-de-participantes-do-str) ou na nossa [API de instituições](https://docs.openbank.stone.com.br/reference#overview-institui%C3%A7%C3%B5es). 
{{</ faq >}}

{{< faq "Quais adquirentes/subadquirentes pagam na Conta Stone?" >}}
Sim! Hoje é possível cadastrar sua Conta Stone para receber pagamentos da: Acqio, Bin, Cielo, GetNet, Gympass, Ifood, Moip, PagSeguro, PicPay, Stelo, Stone e SumUp. 
{{</ faq >}}

{{< faq "Que bandeiras/vouchers posso receber na Conta Stone?" >}}
Hoje é possível direcionar os recebíveis das seguintes bandeiras/vuchers para sua Conta Stone: Visa, Mastercard, Elo, Amex, Hiper, Cabal Sodexo, VR, Ticket, Green Card, Coopecard, Verocard e Ben.
{{</ faq >}}

