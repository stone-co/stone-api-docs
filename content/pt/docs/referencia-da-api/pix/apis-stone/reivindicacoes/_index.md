---
title: "Reinvindicação de Chaves Pix"
linkTitle: "Reinvindicação de Chaves Pix"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T11:00:00-03:00
weight: 3
draft: false
description: >
  Entenda como funcionam as Reinvincações de Chaves Pix!
---

## O que é uma Reinvindicação de Chave Pix
---

Cada Chave PIX pode ser cadastrada em uma única conta. Se a cliente quer cadastrar uma chave em uma conta A, mas essa chave já está cadastrada em uma conta B, ela vai cair em um dos cenários abaixo:
<br><br>
1- **Fluxo de Portabilidade:** Conta A e conta B pertencem à mesma titular, mas estão em PSPs (Prestador do Serviço de Pagamento) diferentes, mas pertencem à mesma titular. Ex.: cliente possui uma Conta Stone e uma conta no Banco XPTO (mesma titularidade) e deseja cadastrar na sua Conta Stone uma chave já cadastrada no Banco XPTO, ou vice e versa.
<br><br>
2- **Alteração de Chave:** Conta A e conta B pertencem à mesma titular e estão no mesmo PSP. Ex.: cliente possui duas Contas Stone em seu nome (mesma titularidade) e deseja cadastrar na sua conta PF uma chave já cadastrada em sua conta PJ
<br><br>
3- **Reivindicação de Posse:** Conta A e conta B pertencem a titulares diferentes. Aqui, temos dois tipos:
  a. Conta A e Conta B estão no mesmo PSP
  b. Conta A e Conta B estão em PSPs diferentes
<br><br>
Em todos os casos, falamos da figura do PSP que vai ceder a chave (PSP Doador, dono da conta B no nosso exemplo), e o PSP que quer receber e ficar com a chave (PSP Reivindicador, dono da conta A no nosso exemplo).
<br><br>


{{% pageinfo %}}
**Atenção!**<br>Não é possível cadastrar a mesma chave em mais de uma instituição. <br>Se a cliente desejar transferir uma Chave Pix de uma instituição para outra, ela pode pedir a portabilidade dessa chave (com exceção da chave aleatória, que é intransferível) ou excluir a chave em uma instituição, e cadastrá-la na desejada.
{{% /pageinfo %}}
<br>

## Principais Regras do BACEN 
---
<br>
1- Durante qualquer pedido de reivindicação, do momento em que o DICT coloca o status do pedido em “Aberto” até o momento em que o DICT(Diretório de Identificadores de Contas Transacionais) altera o status para “Completo”, a chave Pix não não pode ser nem registrada, nem excluída. O pedido de reivindicação em si pode ser cancelado se:
<br>
    - O usuário reivindicador (que começou o pedido) quiser cancelar;
    - Algum dos PSPs envolvidos perceber uma suspeita de fraude e quiser cancelar.
<br><br>
**Sobre portabilidade:** o usuário doador (dono da conta B no nosso exemplo, que já está com a chave) tem até 7 dias para cancelar ou confirmar um pedido de reivindicação do tipo portabilidade. Se ele não responder, o PSP Doador deve deve necessariamente cancelar o pedido.

<br><br>
**Sobre reivindicação de posse:** O usuário doador (dono da conta B no nosso exemplo, que já está com a chave) tem até 7 dias para cancelar ou confirmar um pedido de reivindicação do tipo posse. Se ele não responder, o PSP Doador deve deve necessariamente confirmar o pedido.
  - Depois desses 7 dias a gente entra no "período de encerramento", também de 7 dias, onde o usuário doador ainda pode validar a posse da chave e cancelar a reivindicação. Nesse caso, o PSP Doador deve cancelar o processo, por indício de fraude.
  - Se o usuário doador não validar a posse da chave até o final do "período de encerramento", o PSP Reivindicador deve solicitar uma nova validação de posse do seu usuário (dono da conta A, que quer a chave) e, depois essa validação, completar o pedido no DICT.
 - Se o usuário reivindicador não fizer a validação de posse até o 30º dia após o início do processo de reivindicação, o PSP Reivindicador deve necessariamente cancelar a solicitação no DICT. 
 <br>
Nós consultamos pelo menos uma vez por minuto o serviço de reivindicação do DICT para ver se existem mudanças nos status de pedidos de reivindicação do tipo portabilidade que nos envolvem (tanto como reivindicador quanto como doador), ou que envolvem algum participante indireto nosso.


##### Status da reivindicação

- `open`: aberta pelo reivindicador, mas ainda não recebida pelo doador.
- `waiting_resolution`: reivindicação já foi recebida pelo doador e está aguardando a resolução. Os critérios confirmação ou cancelamento da reivindicação seguem normas específicas a depender do tipo (posse ou portabilidade).
- `confirmed`: doador confirmou a reivindicação. Isso implica a remoção da chave do DICT e da base interna do PSP doador. Está aguardando o reivindicador encerrar o processo.
- `cancelled`: doador ou reivindicador cancelou a reivindicação, mantendo o vínculo inalterado (conforme estava antes da reivindicação) tanto no DICT quanto na base interna do PSP.
- `completed`: tanto o DICT quanto o reivindicador atualizaram suas bases com o novo vínculo.
<br> <br> <br>

Para manusear as chaves, clique nos links abaixo:
