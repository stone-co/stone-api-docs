---
title: "Pagando com Pix"
linkTitle: "Pagando com Pix"
date: 2021-06-16T12:03:51-03:00
lastmod: 2021-06-16T12:03:51-03:00
weight: 1
draft: false
description: >
  Como fazer pagamentos com Pix
---

O Pagamento de um Pix pode ser feito através da inserção dos dados completos do recebedor, por meio da inserção de uma chave Pix ou pela leitura de um QR code.

<br>

#### **Fluxo para criação de envio de Pix através dos dados da conta destino**
---
<br>

1. Realiza request através do [endpoint]({{< relref "/docs/referencia-da-api/pix/pagamento/criar-pagamento-pendente/">}}) /api/v1/pix/outbound_pix_payments enviando parâmetros validos. Este irá retornar uma resposta com os dados do Pix.
2. Realiza request através do [endpoint]({{< relref "/docs/referencia-da-api/pix/pagamento/confirmar-pagamento-pendente/">}}) /api/v1/pix/outbound_pix_payments/{id}/actions/confirm informando o campo `id` retornado pela resposta desse passo 1.<br><br>


#### **Fluxo de criação de envio de Pix através da leitura do QRCode**
---
<br>

1. Realiza request através do [endpoint]({{< relref "/docs/referencia-da-api/pix/pagamento/buscar-dados-qrcode/">}}) /api/v1/outbound_pix_payments/brcode informando o QRCode através do campo `brcode`. Este irá retornar uma reposta com os dados do QRCode.
2. Realiza request através do [endpoint]({{< relref "/docs/referencia-da-api/pix/pagamento/criar-pagamento-pendente/">}}) /api/v1/pix/outbound_pix_payments enviando parâmetros validos. Este irá retornar uma resposta com os dados do Pix.
3. Realiza request através do [endpoint]({{< relref "/docs/referencia-da-api/pix/pagamento/confirmar-pagamento-pendente/">}}) /api/v1/pix/outbound_pix_payments/{id}/actions/confirm informando o campo `id` retornado pela resposta desse passo 2.<br><br
