---
title: "Criar Reivindicação/Portabilidade"
linkTitle: "Criar Reivindicação/Portabilidade"
date: 2022-11-21T11:00:00-03:00
lastmod: 2022-11-21T1:00:00-03:00
weight: 8
draft: true
description: >

---
Caso uma chave esteja em posse de uma outra conta e um usuário tente realizar a criação dela, este processo resultará em uma falha. Neste caso, o usuário pode realizar o processo de reivindicação de uma chave Pix.

Este  processo pode ocorrer tanto para uma chave que pertence ao mesmo  indivíduo/organização (possui o mesmo CPF ou CNPJ) quanto para uma chave  que está em posse de uma pessoa física/jurídica distinta.

No primeiro caso, realiza-se um processo de portabilidade (portability), enquanto no segundo é realizado um processo de Reivindicação de Posse (ownership).

Nem todas as chaves podem passar pelos mesmos processos de transferência entre contas. 
 
 **- Reivindicação de Posse**: `E-mail`, `Celular`
 <br>
 **- Portabilidade**: `E-mail`, `Celular`, `CPF`, `CNPJ`
<br><br>

##### **Webhook**


##### **Request**


GET /api/v1/pix/:account_id/entry_claims
```
Parâmetros para query.
```
- "pix_entry_id" * (obrigatorio)
- "participant_ispb" *(obrigatório para participantes indiretos)
- "beneficiary_account"
- "beneficiary_account.branch_code"
- "beneficiary_account.account_code"
- "beneficiary_account.account_type"
- "beneficiary_account.created_at"
- "beneficiary_entity"
- "beneficiary_entity.name"
- "beneficiary_entity.legal_name"
- "beneficiary_entity.document_type"
- "beneficiary_entity.document"   
```

```
POST - /pix/:account_id/entry_claims/
content-type: application/json
```