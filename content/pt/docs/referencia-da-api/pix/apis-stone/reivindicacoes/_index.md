---
title: "Reivindicação de Chaves Pix"
linkTitle: "Reivindicação de Chaves Pix"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T11:00:00-03:00
weight: 3
draft: false
description: >
  Entenda como funcionam as Reivindicações de Chaves Pix!
---

## O que é uma Reivindicação de Chave Pix
---

Cada Chave Pix pode ser cadastrada em uma única conta. Se um cliente deseja cadastrar uma chave em uma conta A, mas essa chave já está cadastrada em uma conta B, ele vai cair em um dos cenários abaixo:
<br><br>
1- **Fluxo de Portabilidade:** Conta A e conta B pertencem à mesma titular, mas estão em PSPs (Prestador do Serviço de Pagamento) diferentes. Ex.: cliente possui uma Conta Stone e uma conta no Banco XPTO (mesma titularidade) e deseja cadastrar na sua Conta Stone uma chave já cadastrada no Banco XPTO, ou vice e versa.
<br><br>
2- **Reivindicação de Posse:** Conta A e conta B pertencem a titulares diferentes. Aqui, temos dois tipos:
  1. Conta A e Conta B estão no mesmo PSP
  2. Conta A e Conta B estão em PSPs diferentes
<br><br>
Em ambos os casos, falamos da figura do PSP que vai ceder a chave (PSP Doador, titular da conta B no nosso exemplo), e o PSP que quer receber e ficar com a chave (PSP Reivindicador, titular da conta A no nosso exemplo).
<br><br>


{{% pageinfo %}}
**Atenção!**<br>Não é possível cadastrar a mesma chave em mais de uma instituição. <br>Se o cliente desejar transferir uma Chave Pix de uma instituição para outra, ela pode pedir a portabilidade dessa chave (com exceção da chave aleatória, que é intransferível) ou excluir a chave em uma instituição, e cadastrá-la na desejada.
{{% /pageinfo %}}
<br>

## Principais Regras do BACEN 
---
<br><br>
Durante qualquer pedido de reivindicação, do momento em que o DICT coloca o status do pedido em “Aberto” até o momento em que o DICT (Diretório de Identificadores de Contas Transacionais) altera o status para “Completo”, a chave Pix não pode ser nem registrada, nem excluída. O pedido de reivindicação em si pode ser cancelado se:
<br>
  1. O usuário reivindicador (que começou o pedido) quiser cancelar;
  2. Algum dos PSPs envolvidos perceber uma suspeita de fraude e quiser cancelar.
<br><br>

**Sobre portabilidade:** o usuário doador (titular da conta B no nosso exemplo, que já está com a chave) tem até 7 dias para cancelar ou confirmar um pedido de reivindicação do tipo portabilidade. Se ele não responder, o PSP Doador deve deve necessariamente cancelar o pedido.
<br>

**Sobre reivindicação de posse:** O usuário doador (titular da conta B no nosso exemplo, que já está com a chave) tem até 7 dias dias para cancelar ou confirmar um pedido de reivindicação do tipo posse. Se ele não responder, o PSP Doador deve deve necessariamente confirmar o pedido.
  - Depois desses 7 dias a a Stone entra no "período de encerramento", também de 7 dias, onde o usuário doador ainda pode validar a posse da chave e cancelar a reivindicação. Nesse caso, o PSP Doador deve cancelar o processo, por indício de fraude.
  - Se o usuário doador não validar a posse da chave até o final do "período de encerramento", o PSP Reivindicador deve solicitar uma nova validação de posse do seu usuário (titular da conta A, que deseja posse a chave) e, depois dessa validação, completar o pedido no DICT.
 - Se o usuário reivindicador não fizer a validação de posse até o 30º dia após o início do processo de reivindicação, o PSP Reivindicador deve necessariamente cancelar a solicitação no DICT. Quando isso ocorre, a posse não ficará com nenhuma das duas instituições.
 <br>
Nós consultamos com alta frequência o serviço de reivindicação do DICT para ver se existem mudanças nos status de pedidos de reivindicação do tipo portabilidade que nos envolvem (tanto como reivindicador quanto como doador), ou que envolvem algum participante indireto nosso.


##### Status da reivindicação

- `open`: aberta pelo reivindicador, mas ainda não recebida pelo doador.
- `waiting_resolution`: reivindicação já foi recebida pelo doador e está aguardando a resolução. Os critérios confirmação ou cancelamento da reivindicação seguem normas específicas a depender do tipo (posse ou portabilidade).
- `confirmed`: doador confirmou a reivindicação. Isso implica a remoção da chave do DICT e da base interna do PSP doador. Está aguardando o reivindicador encerrar o processo.
- `cancelled`: doador ou reivindicador cancelou a reivindicação, mantendo o vínculo inalterado (conforme estava antes da reivindicação) tanto no DICT quanto na base interna do PSP.
- `completed`: tanto o DICT quanto o reivindicador atualizaram suas bases com o novo vínculo.
<br> <br> <br>

Os endpoints relativos a reivindicação e portabilidade estão listados abaixo:
