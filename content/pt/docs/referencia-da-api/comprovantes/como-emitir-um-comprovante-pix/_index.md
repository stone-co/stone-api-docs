---
title: "Emitir Um Comprovante Pix"
linkTitle: "Emitir Um Comprovante Pix"
slug: "emitir-um-comprovante-pix"
hidden: false
date: 2021-08-23T18:34:00-03:00
lastmod: 2021-08-23T18:34:00-03:00
description: >
---

Comprovantes informam sobre uma transação em detalhes, como fonte, destinatário e estado.

Nesse endpoint, vamos gerar comprovantes de Pix enviados e que estejam em estados de sucesso, como finalizado e agendado.

```
POST https://sandbox-api.openbank.stone.com.br/api/v1/exports/receipts
```

---

#### **BODY PARAMS**

---

**resource_type*** `string`
<br>Allowed values: `pix_payment`, `outbound_pix_payment`, `refund_for_pix_payment`, `refund_for_outbound_pix_payment` e `refund_reversal_for_pix_payment`

**resource_id*** `string`
<br>Format: `UUID`

<br><br>

---

#### **HEADERS**

---

**x-stone-idempotency-key** `string`

**authorization** `string`
<br>Bearer token

<br><br>

---

#### **Response**

```
200 OK
content-type: application/pdf
```

Retorna o PDF do comprovante
