---
title: "O Que É Um Pagamento"
slug: "o-que-é-um-pagamento"
hidden: false
date: "2019-05-02T21:01:36.255Z"
lastmod: "2021-02-01T22:02:27.916Z"
weight: 1
---
---
<br>

### Conceito
---

<br>

Oferecemos uma API de Pagamentos, através da qual é possível efetuar o pagamento de contas com código de barras como, por exemplo, boletos, contas de luz, água, gás, IPTU, IPVA, entre outras.

Nossa API suporta pagamentos de todos os boletos CIP e um grande número de concessionárias/tributos. A janela de pagamentos de concessionárias pode variar de acordo com a empresa emissora. Pagamentos processados após o horário limite imposto pelo emissor serão acolhidos no dia útil seguinte.

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A API de Pagamentos fica disponível todos os dias das 00h00 até 23h50. Boletos pagos após 23h50 serão acolhidos no dia útil seguinte.		
{{< /alert >}}


<br>

### Estados
---

<br>

Segue abaixo os estados possíveis de um **pagamento**: 

<br>

![Imagem 1](/docs/referencia-da-api/pagamentos/o-que-e-um-pagamento/estados_pagamento.png)

<br>



### Falhas em Pagamentos

---

<br>

Falha é qualquer erro que ocorra entre a criação e a movimentação do dinheiro na conta. Ou seja, qualquer condição que era válida no momento da criação do pagamento, mas que mudou nas etapas seguintes.

A seguir listamos algumas das falhas possíveis para operações de pagamento.

<br>


| Código | Descrição                                                                  |
| ------ | -------------------------------------------------------------------------- |
| 0      | Ocorreu um erro durante o pagamento. Por favor, tente novamente.           |
| 1      | Saldo insuficiente.                                                        |
| 2      | Pagamento sem valor registrado não é suportado. Contate o emissor.         |
| 3      | Pagamento para titularidade diferente não suportado. Conclua seu cadastro. |
| 4      | Pagamento sem valor registrado não é suportado. Contate o emissor.         |


<br>



### Reembolsos em Pagamentos
---

<br>

Abaixo listamos algumas das razões possíveis para ocorrer reembolsos, como também seus códigos correspondentes.

<br>

| Código | Descrição                                                                  |
| ------ | -------------------------------------------------------------------------- |
| 40     | Código de moeda inválido.                                                  |
| 51     | Boleto de pagamento liquidado com valor maior ou menor do que o permitido. |
| 52     | Boleto vencido sem os juros/multa devidos.                                 |
| 53     | Código de barras não pertence ao banco emissor do boleto.                  |
| 63     | Código de barras inválido.                                                 |
| 68     | Boleto pago em duplicidade                                                 |
| 69     | Boleto pago em duplicidade.                                                |
| 70     | Por solicitação do cliente do banco recebedor do boleto.                   |
| 71     | Valor inválido.                                                            |
| 73     | Beneficiário não cadastrado no banco emissor.                              |
| 74     | Beneficiário com CPF/CNPJ divergente do cadastro no banco emissor.         |
| 75     | Pagador com CPF/CNPJ divergente do cadastro no banco emissor.              |
| 76     | Cópia não encaminhada pelo banco recebedor no prazo previsto.              |



---
