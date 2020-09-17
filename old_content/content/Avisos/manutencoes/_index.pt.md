---
title: "Manutenções"
date: 2020-05-14T10:17:00-03:00
lastmod: 2020-05-14T10:17:00-03:00
weight: "1"
draft: false
---

#### Manutenção programada Stone

Faremos uma manutenção interna no dia 07/06 entre 02:30 e 05:00, com isso pode ocorrer uma lentidão no processamento de pagamentos e registro de boletos e o serviço de dry-run de pagamentos retornará prenchido apenas os campos do objeto "barcode_details".

* Data: 07/06, 02:30 - 05:00
* Ambiente: Produção
* Serviços: Dry-Run Pagamento, Pagamento, Emissão de boletos
* Impacto: Os serviços/APIs continuarão acatando os requests normalmente, mas poderá ocorrer uma lentidão na finalização de pagamentos e registro de boletos emitidos. Além disso, os campos do objeto pagamento do dry-run retornarão vazios.
<br>
<br>
<br>
<br>
---
#### Manutenção programada PCR

A Plataforma Centralizada de Recebíveis (PCR) fará uma manutenção programada no sábado 06/06 entre 22h e 23h59.  A PCR é o sistema da CIP específico de boletos e com isso é esperada uma lentidão no processamento de pagamentos e registro de boletos e o serviço de dry-run de pagamentos retornará prenchido apenas os campos do objeto "barcode_details".

* Data: 06/06 05, 22h - 23h59
* Ambiente: Produção
* Serviços: Dry-Run Pagamento, Pagamento, Emissão de boletos
* Impacto: Lentidão nos serviços de Pagamentos e Registro de boletos emitidos. Os campos do objeto pagamento do dry-run retornarão vazios. 
