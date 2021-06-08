---
title: "O que é um Link de Pagamento"
linkTitle: "O Que É Um Link De Pagamento"
date: 2021-03-10T15:30:00-03:00
lastmod: 2021-03-10T16:30:00-03:00
weight: 1
description: >
---

---

<br>

É uma funcionalidade da Conta Stone que permite criar links de pagamentos que podem ser compartilhados para a realização de vendas à distância. 

O link é uma funcionalidade padrão da Conta Stone que é habilitada no momento em que o usuário é aprovado no KYC. 

Cada Conta Stone estará apta a gerar e gerenciar seus próprios links de pagamentos, independentemente de ser de um usuário ou uma organização.

<br>

#### **Status do link de pagamento**
---
<br>

Todo link de pagamento nasce como "_**Criado**_" e tem um tempo de expiração que inativa qualquer operação sobre aquele link de pagamento, nesse momento ele assume um status de "_**Expirado**_".

Um link de pagamento que não tiver sido pago ou que não tenha sido expirado pode ser cancelado a qualquer momento, assumindo status de "_**Cancelado**_". Tanto a cobrança expirada quanto a cancelada terão o status da order como "_**Canceled**_". A forma inicial de identificar que
é um caso ou outro é pelo campo closed.

<br>

##### **Toda transação cancelada é fechada e depois cancelada**

```Json
{
	"status": "Canceled",
	"closed": "true"
}
```
<br>

##### **Toda transação expirada se mantém aberta (closed: false), mas com status alterado para cancelado**

```Json
{
	"status": "canceled",
	"closed": "false"
}
```