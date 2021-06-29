---
title: "Chamada autenticada"
linkTitle: "Chamada autenticada"
date: 2021-06-28T14:00:00-03:00
lastmod: 2021-06-28T14:00:00-03:00
weight: 5
description: >

---
<br>

Após realizar o processo de [Autenticação](/docs/guias/token-de-acesso/autenticacao/) e receber como resposta o seu Token de Acesso, basta colocá-lo no header Authorization. Você irá usar o valor recebido para preenchimento do  Bearer ACCESS_TOKEN.

Para realizar chamadas autenticadas em nossa API, disponibilizamos as seguintes URLs: <br><br>


| Ambiente | Endpoint de Acesso |
| -------- | ------------------ |
| Sandbox | https://sandbox-api.openbank.stone.com.br |
| Produção | https://api.openbank.stone.com.br |


{{% pageinfo %}}
**Não solicite um token por chamada!**

O access_token possui duração de 15 minutos e você deve utilizar esse mesmo token durante todo seu período de utilização, não importa quais e quantas chamadas diferentes sua aplicação irá fazer nesse período.

{{% /pageinfo %}}


A seguir, vamos te guiar pela seção [Conta de Pagamento](/docs/guias/conta-de-pagamento/), onde você poderá entender mais sobre as características do nosso negócio e sobre o processo de abertura de conta.
