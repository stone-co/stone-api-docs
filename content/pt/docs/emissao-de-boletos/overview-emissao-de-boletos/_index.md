---
title: "Overview Emissão de Boletos"
slug: "overview-emissao-boleto"
draft: false
weight: 1
date: "2020-03-30T07:01:34.376Z"
lastmod: "2020-12-23T13:10:22.067Z"
---

Nessa API, os boletos são separados em três grupos que apresentam regras de funcionamento diferentes: Depósito, Proposta e Cobrança. Veja abaixo os grupos e seus tipos.


#### Depósito

Tem como objetivo fazer um deposito na conta pelo próprio dono da conta. 

Tipo (type):
- `deposit`


#### Proposta

Tem como objetivo apresentar uma proposta a um terceiro. Não tem caráter de cobrança.

Tipo (type):
- `proposal`


#### Cobrança

Tem como objetivo cobrar um terceiro. Tem caráter oficial de cobrança. Existem tipos de cobrança específicos de acordo com atividade que está orginando a cobrança. Abaixo veremos a lista dos tipos disponíveis. <br>
Importante ressaltar que pode haver restrição de habilitação de um determinado tipo para uma conta de acordo com as atividades listadas para esse CNPJ em seu registro ofical (CNAE).

Tipo (type):
- `bill_of_exchange`
A duplicata mercantil é especifica para cobranças advindas de vendas de produtos. 

- `tuition_payment`
Específico  para cobranças advindas de mensalidades escolares.
