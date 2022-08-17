---
title: "Old_Especificação do QR Code"
linkTitle: "Old_Especificação do QR Code"
date: 2020-11-06T15:07:33-03:00
lastmod: 2020-11-06T15:07:33-03:00
weight: 5
draft: true
description: >
   
---

##### **Formatos retornados e content type**
![Imagem 1](https://user-images.githubusercontent.com/11000135/98400401-b6b24980-2042-11eb-8a59-1c6e56410530.png)
![Imagem 2](https://user-images.githubusercontent.com/11000135/98400393-b31ec280-2042-11eb-9c51-0deb65dcc0a1.png)

##### **Sequência de caracteres correspondente ao payload do QR Code dinâmico**
```
000201
010212
2674
  0014br.gov.bcb.pix
  2552example.com/pix/8b3da2f3-9a41-40d1-a91a-bd93113bd441
52040000
5303986
5406123.45
5802BR
5913Fulano de Tal
6008BRASILIA
6219
  0515RP12345678-2019
6304FF24 

```

##### **QR Code dinâmico gerado**
![Respectivo QR Code dinâmico](https://user-images.githubusercontent.com/11000135/98400400-b5811c80-2042-11eb-9de3-a69107edf803.png)

##### **Referência**
https://www.bcb.gov.br/content/estabilidadefinanceira/pix/Regulamento_Pix/II.ManualdePadroesparaIniciacaodoPix-versao2.0.pdf