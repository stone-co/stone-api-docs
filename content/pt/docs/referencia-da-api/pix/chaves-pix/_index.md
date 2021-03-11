---
title: "Chaves PIX"
linkTitle: "Chaves PIX"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 1
description: >
  Entenda como funcionam as Chaves PIX!
---

## O que é uma Chave PIX

No arranjo do PIX os usuários, tanto pagadores quanto recebedores, precisam se cadastrar no DICT (Diretório de Identificadores de Contas Transacionais) para criar sua(s) chave(s) PIX. 
<br><br>
Esse cadastro é feito por meio de um PSP (Prestador do Serviço de Pagamento)  direto ou indireto do arranjo, assim toda vez que essa chave for usada o dinheiro será direcionado para a conta do recebedor nesse PSP.
<br><br>
Essas chaves serão usadas pelos PSP diretos e indiretos na comunicação com os sistemas do PIX para o processamento das transações. 
<br><br>
Os PSPs diretos e indiretos por sua vez são cadastrados e homologados junto ao PIX e por isso possuem um cadastro diferente não tendo uma Chave PIX. Na API de Banking vamos identificar o PSP indireto em todos os requests por do `account_id` e do  `participant_ispb`.
<br> <br> <br>

## Tipos de Chave PIX

Para fazer o cadastro dessa chave os usuários podem optar por 4 tipos diferentes:<br>
- **Telefone celular** |  `phone`: cada número de celular do usuário pode ser cadastrado uma única vez com uma única instituição.<br>
- **Documento** | `CPF`, `CNPJ`: só pode ser cadastrado uma única vez com uma única instituição.<br>
- **E-mail** | `email`: cada email do usuário pode ser cadastrado uma única vez com uma única instituição.<br>
- **Chave aleatória / EVP** | `random_key`: é uma sequência alfa numérica aleatória gerada automaticamente pelo DICT mais utilizada no fluxo de QR Code. O usuário pode usar 1 chave aleatória por PSP seja indireto ou direto.<br>
<br>
Um usuário pessoa física poderá ter no máximo 5 Chaves PIX por conta, enquanto um usuário do tipo pessoa jurídica pode ter até 20 Chaves PIX por conta.Os dois devem respeitar os limites de cada tipo.
<br><br>
O conjunto de chaves de um participante indireto é independente do conjunto de chaves do particpante direto que ele usa como fornecedor. Ou seja, no caso de um usuário que usa um PSP indireto, mas também é cliente do PSP direto que age como fornecedor do indireto, o usuário terá no mínimo duas chaves PIX, uma atrelada ao participante direto e outra atrelado ao participante indireto. 
<br>


