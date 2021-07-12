---
title: "Valores"
linkTitle: "Valores"
date: 2021-07-12T11:20:05-03:00
lastmod: 2021-07-12T11:20:05-03:00
weight: 4
description: >

---

## Valores Percentuais

Alguns endpoints precisam receber ou retornar valores percentuais. Para evitar problemas de
representação e de arredondamento, convencionamos de usar uma estrutura pra evitar
strings e floats.

A estrutura tem o seguinte formato:

**coeficient*** `int32`
<br> Coeficiente do cálculo do percentual

---

**exponent*** `int32`
<br> Expoente do cálculo do percentual

---

Essa estrutura é usada com a fórmula

<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

$$percentage = coeficient*10^{exponent}$$

Por definição 100% = 100 * (1/100) = 1. De forma análoga, 70% pode ser representado como
`coefficient = 70, exponent = -2`, ou como `coefficient = 7, exponent = -1`

---

## Valores Financeiros

Todos os valores na API serão sempre inteiros e expressos em centavos de Reais.

Assim, o valor de um real (R$1,00) ficaria: `100`.