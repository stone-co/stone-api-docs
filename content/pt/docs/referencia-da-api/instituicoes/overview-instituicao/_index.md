---
title: "Overview Instituições"
linkTitle: "Overview Instituições"
slug: "overview-instituições"
draft: false
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 1
description: >
---

---

<br>

Esta API possibilita que haja a consulta de Instituições de Pagamento Autorizadas, Bancos de Desenvolvimento, Investimento, Câmbio e Bancos Múltiplos sem carteira comercial. Isso possibilitará que o usuário possa visualizar as Instituições e Bancos que estão aptos a receber transferências financeiras.

<br>

#### Listar todas as instituições e bancos
---
<br>

Possibilitamos que a aplicação parceira possa listar todas as Instituições e Bancos. Nela há o retorno das informações referentes a nome completo e nome simplificado, Código ISPB (8 dígitos) e código numérico, frequentemente utilizado como identificador único dos Bancos e Instituições.

<br>

#### Busca por código numérico
---
<br>

Possibilitamos também que haja a busca de apenas um Banco ou Instituição pelo código numérico. É necessário apenas que haja a inserção do seu código no header da requisição.

<br>

{{< alert title="Atenção" >}}
<br>

Os pagamentos de ID (Instituição domicilio) são processados em dias úteis às 07h50 da manhã.
{{< /alert >}}
