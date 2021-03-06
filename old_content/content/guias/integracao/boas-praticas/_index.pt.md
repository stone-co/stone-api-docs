---
title: "Boas Práticas"
date: 2020-05-14T14:46:51-03:00
lastmod: 2020-05-14T14:46:51-03:00
weight: "1"
draft: false
---

### Tokens JWT

Tokens JWT são dados sensíveis, assim como senhas ou dados de cartões de crédito. Por isso, é de extrema importância manusear e armazenar esses dados corretamente.

#### Não armazene tokens no *local storage*

O armazenamento local de um Browser não é um lugar seguro para se armazenar dados sensíveis. Dados armazenados no local storage podem:

* Ser acessados via Javascript;
* Ser vulneráveis a Cross-Site Scripting.

#### Caso um backend esteja disponível

Se sua Aplicação tem um backend disponível, os tokens devem ser manuseados server-side.

#### Caso um backend não esteja disponível

Se sua Aplicação é uma Single Page Application, a Aplicação deve requisitar os tokens e armazená-los em memória sem nenhuma persistência. Faça as chamadas de API usando os tokens armazenados em memória.

Para outros casos, informações sobre boas práticas com Tokens JWT estão disponíveis [aqui](https://auth0.com/docs/security/store-tokens).

### Idempotência

Nossos endpoints que envolvem operações financeiras suportam [Idempotência](https://pt.wikipedia.org/wiki/Idempot%C3%AAncia). Existe a possibilidade de ocorrer operações duplicadas, como, por exemplo, com a queda de conexão 3G durante a realização de uma operação. Para evitar que a mesma operação ocorra mais de uma vez no nosso sistema, sempre envie o cabeçalho de Idempotência (x-stone-idempotency-key).

Observe abaixo cada caso possível em relação à **chave de idempotência** e seus retornos:

* Uma chamada com **outra chave de idempotência**, **independente do corpo da requisição**, será tratada como uma nova requisição.
* Uma chamada com a **mesma chave de idempotência** e o **mesmo corpo da requisição** retornará a mesma resposta que foi recebida anteriormente, devido a um cache.
  Se isso ocorrer em um período curto demais pode ocasionar uma resposta `HTTP 423`, indicando que o recurso está travado e que a requisição original ainda está em processamento. Neste caso, é necessária uma retentativa desta chamada.
* Uma chamada com a **mesma chave de idempotência** e com o **corpo da requisição diferente do original** retornará um erro de idempotência `HTTP 409`.

### Simulações (dry-run)

Nossos endpoints que envolvem operações financeiras suportam [Simulações (dry-run)](https://docs.openbank.stone.com.br/reference#simular-uma-transfer%C3%AAncia-interna), permitindo que a usuária visualize com antecedência o que vai acontecer nessa operação.

Em alguns casos, as Simulações permitem enriquecer os dados de uma operação, como, por exemplo o [Pagamento de Boletos](https://docs.openbank.stone.com.br/reference#simular-o-pagamento-de-um-documento).