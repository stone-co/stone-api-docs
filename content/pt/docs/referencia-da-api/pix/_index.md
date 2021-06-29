---
title: "PIX (Alpha)"
linkTitle: "PIX (Alpha)"
lastmod: 2021-03-31T18:00:00-03:00
weight: 16
draft: false
description: >
---      
---
<br>

{{% pageinfo %}}
A integração com o Pix ainda está em Alpha, o que significa que temos um grupo pequeno de parceiros testando a funcionalidade para que possamos fazer ajustes e então liberar para todos os parceiros.
{{% /pageinfo %}}

<br>

#### **O que é o Pix?**
---
<br>

O Pix é a nova modalidade de pagamentos instantâneos do Banco Central, que entrou em vigor no Brasil inteiro no dia 16 de novembro de 2020. 

Além de sua ampla grade de funcionamento e pequeno tempo de processamento, o Pix busca simplificar a experiência do usuário que consegue passar o dinheiro para outro participante informando apenas seu telefone, documento (CPF/CNPJ), seu email ou lendo um QR Code. Lembrando que também é possível fazer um Pix informando os dados bancários, como é feito em uma TED.

<br>

{{< alert title="Horário de funcionamento" >}}
<br>

A API de Pix fica disponível todos os dias da semana e 24 horas por dia, pois é uma modalidade de pagamento instantânea.	
{{< /alert >}}

<br>

#### **Participantes do Pix**
---
<br>

O Pix tem quatro tipos de participantes principais:<br><br>
- **Participante Direto (PSP direto)**: Instituição homologada junto ao Banco Central (BC) que fará o processamento do Pix junto aos sistemas do BC tanto do ponto de vista informacional, quanto do ponto de vista financeiro. Ou seja, além de ser responsável por toda a troca de informação com os sistemas do Pix, quando agindo como instituição do pagador será a instituição que enviará o dinheiro para o BC e quando agindo como instituição do recebedor receberá o dinheiro do BC. Fazendo um comparativo com o arranjo de cartões seria mais ou menos o equivalente a adquirência e o emissor dependendo se estamos agindo ao lado do recebedor ou do pagador respectivamente. <br>
- **Participante Indireto (PSP indireto)**: Instituição homologada junto ao Banco Central que fará parte do arranjo do Pix tanto do ponto de vista informacional, quanto do ponto de vista financeiro, mas que usará um participante direto para fazer a intermediação da integração com os sistemas do Pix. Fazendo um comparativo com o arranjo de cartões seria mais ou menos o equivalente a uma subadquirente. <br>
- **Usuário Recebedor**: é quem vai receber o dinheiro da transação que está sendo efetuada. Fazendo um comparativo com o arranjo de cartões, seria mais ou menos o equivalente ao lojista. <br>
- **Usuário Pagador**: é quem vai pagar a transação que está sendo efetuada. Fazendo um comparativo com o arranjo de cartões seria mais ou menos o equivalente ao comprador / dono do cartão.<br><br>



#### **Status de um Pix**
---
<br>

Os status possiveis são: `CREATED`, `CONFIRMED`, `FAILED`, `MONEY_RESERVED`, `REFUNDED` e `SETTLED`. A partir do momento que um Pix é criado, ele **nunca expira**.

- `CREATED` -  Significa que o Pix foi criado e está aguardando confirmação.

- `CONFIRMED` - Significa que o Pix que foi criado e estava com o status `CREATED`, foi confirmado.

- `MONEY_RESERVED` - Significa que o Pix que foi confirmado e estava com o status `CONFIRMED`, teve o dinheiro retirado da conta do cliente e reservado em uma conta gráfica a parte para a operação.

- `SETTLED` - Significa que o Pix que estava com o estado de `MONEY_RESERVED`, foi finalizado e liquidamos o dinheiro reservado na conta gráfica da operação.

- `REFUNDED` - Significa que o Pix que estava com o estado de `MONEY_RESERVED`, foi rejeitado ou devolvido.

- `FAILED` - Significa que o Pix que estava com o estado de `CONFIRMED`, falhou no momento de reservar o dinheiro, podendo ser devido a falta de saldo do cliente, e portanto ele vai para o estado de `FAILED` e o fluxo da operação se encerra.<br><br>



#### **API Pix do BACEN**
---
<br>

Para determinados casos, é possível utilizar a API de Pix do BACEN. Para acessá-la, clique [aqui](https://bacen.github.io/pix-api/index.html )





<br><br>

##### Para realizar transações com Pix, siga de acordo com o menu abaixo: