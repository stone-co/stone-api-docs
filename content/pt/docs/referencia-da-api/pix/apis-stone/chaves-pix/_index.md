---
title: "Chaves Pix"
linkTitle: "Chaves Pix"
date: 2021-07-15T14:00:00-03:00
lastmod: 2021-07-15T14:00:00-03:00
weight: 3
draft: false
description: >
  Entenda como funcionam as Chaves Pix!
---

## O que é uma Chave Pix
---

No arranjo do Pix os usuários, tanto pagadores quanto recebedores, precisam se cadastrar no DICT (Diretório de Identificadores de Contas Transacionais) para criar sua(s) chave(s) Pix.
<br><br>
Esse cadastro é feito por meio de um PSP (Prestador do Serviço de Pagamento)  direto ou indireto do arranjo, assim toda vez que essa chave for usada o dinheiro será direcionado para a conta do recebedor nesse PSP.
<br><br>
Essas chaves serão usadas pelos PSP diretos e indiretos na comunicação com os sistemas do Pix para o processamento das transações.
<br><br>
Os PSPs diretos e indiretos por sua vez são cadastrados e homologados junto ao Pix e por isso possuem um cadastro diferente não tendo uma Chave Pix. Na API de Banking vamos identificar o PSP indireto em todos os requests por do `account_id` e do  `participant_ispb`.
<br>

{{% pageinfo %}}
**Atenção!**<br>Não é possível cadastrar a mesma chave em mais de uma instituição. <br>Se a cliente desejar transferir uma Chave Pix de uma instituição para outra, ela pode pedir a portabilidade dessa chave (com exceção da chave aleatória, que é intransferível) ou excluir a chave em uma instituição, e cadastrá-la na desejada.
{{% /pageinfo %}}
<br>

## Tipos de Chave Pix
---

Para fazer o cadastro dessa chave os usuários podem optar por 4 tipos diferentes:<br>
- **Telefone celular** |  `phone`: cada número de celular do usuário pode ser cadastrado uma única vez com uma única instituição.<br>Utilizamos o formato internacional: +5561912345678
- **Documento** | `CPF`, `CNPJ`: só pode ser cadastrado uma única vez com uma única instituição.<br>Formato CPF: 12345678900 | Formato CNPJ: 00038166000105
- **E-mail** | `email`: cada email do usuário pode ser cadastrado uma única vez com uma única instituição.<br>Formato: fulano_da_silva.recebedor@example.com | case sensitive
- **Chave aleatória** | `random_key`: é uma sequência alfa numérica aleatória gerada automaticamente pelo DICT mais utilizada no fluxo de QR Code. O usuário pode usar 1 chave aleatória por PSP seja indireto ou direto.<br>Formato: 123e4567-e12b-12d1-a456-426655440000 | case sensitive<br>
<br>

**Regras do BACEN**<br>
Um usuário pessoa física poderá ter no máximo 5 Chaves Pix por conta, enquanto um usuário do tipo pessoa jurídica pode ter até 20 Chaves Pix por conta.Os dois devem respeitar os limites de cada tipo.
<br><br>
O conjunto de chaves de um participante indireto é independente do conjunto de chaves do particpante direto que ele usa como fornecedor. Ou seja, no caso de um usuário que usa um PSP indireto, mas também é cliente do PSP direto que age como fornecedor do indireto, o usuário terá no mínimo duas chaves Pix, uma atrelada ao participante direto e outra atrelado ao participante indireto.
<br> <br> <br>

## Status de uma chave Pix
---

##### Status das solicitações (criação e exclusão)

- `pending`: criação solicitada.
- `accepted`: solicitação finalizada com sucesso.
- `rejected`: solicitação rejeitada. Veja o campo `error_description`para entender o motivo.

<br>

##### Status da chave

- `portability_pending`: o processo de reivindicação de portabilidade está em andamento.
- `claim_requested`: o processo de reivindicação de posse está em andamento.
- `active`: chave ativa no DICT e válida para uso.
- `deleted`: chave excluída no DICT e inválida para uso.

<br>


##### Status da reivindicação

- `open`: aberta pelo reivindicador, mas ainda não recebida pelo doador.
- `waiting_resolution`: reivindicação já foi recebida pelo doador e está aguardando a resolução. Os critérios confirmação ou cancelamento da reivindicação seguem normas específicas a depender do tipo (posse ou portabilidade).
- `confirmed`: doador confirmou a reivindicação. Isso implica a remoção da chave do DICT e da base interna do PSP doador. Está aguardando o reivindicador encerrar o processo.
- `cancelled`: doador ou reivindicador cancelou a reivindicação, mantendo o vínculo inalterado (conforme estava antes da reivindicação) tanto no DICT quanto na base interna do PSP.
- `completed`: tanto o DICT quanto o reivindicador atualizaram suas bases com o novo vínculo.
<br> <br> <br>

Para manusear as chaves, clique nos links abaixo:
