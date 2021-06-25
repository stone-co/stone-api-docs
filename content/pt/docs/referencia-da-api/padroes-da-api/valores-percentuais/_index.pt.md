---
title: "Valores Percentuais"
linkTitle: "Valores Percentuais"
date: 2021-06-25T10:52:05-03:00
lastmod: 2021-06-25T10:52:05-03:00
weight: 5
description: >

---

---
<br>

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

Utilizamos a convenção que 100% = 1, então por exemplo, 70% pode ser representado como
coeficient = 7 e exponent = -1.
