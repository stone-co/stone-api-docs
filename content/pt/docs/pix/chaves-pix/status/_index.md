---
title: "Status"
linkTitle: "Status"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 2
description: >
   
---

#### Status das solicitações (criação e exclusão)

- `pending`: criação solicitada.
- `accepted`: solicitação finalizada com sucesso.
- `rejected`: solicitação rejeitada. Veja o campo `error_description`para entender o motivo. 

<br> <br> 

#### Status da chave

- `portability_pending`: o processo de reivindicação de portabilidade está em andamento. 
- `claim_requested`: o processo de reivindicação de posse está em andamento. 
- `active`: chave ativa no DICT e válida para uso.
- `deleted`: chave excluída no DICT e inválida para uso. 

<br> <br> 


#### Status reivindicação

- `open`: aberta pelo reivindicador, mas ainda não recebida pelo doador.
- `waiting_resolution`: reivindicação já foi recebida pelo doador e está aguardando a resolução. Os critérios confirmação ou cancelamento da reivindicação seguem normas específicas a depender do tipo (posse ou portabilidade).
- `confirmed`: doador confirmou a reivindicação. Isso implica a remoção da chave do DICT e da base interna do PSP doador. Está aguardando o reivindicador encerrar o processo.
- `cancelled`: doador ou reivindicador cancelou a reivindicação, mantendo o vínculo inalterado (conforme estava antes da reivindicação) tanto no DICT quanto na base interna do PSP.
- `completed`: tanto o DICT quanto o reivindicador atualizaram suas bases com o novo vínculo.
