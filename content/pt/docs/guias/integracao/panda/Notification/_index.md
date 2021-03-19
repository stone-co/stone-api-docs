---
title: "Notification"
linkTitle: "Notification"
date: 2021-03-18T15:00:00-03:00
lastmod: 2021-03-18T14:00:00-03:00
weight: 2
draft: true
description: >
---
---

<br>

O Panda possui um módulo para envio de notificações chamado `panda_notifications`. Este módulo contempla toda o tratamento necessário para o envio de uma notificação, desde a coleta de informações até o envio direto das mesmas.

O intuito desta aplicação é enviar notificações a clientes e parceiros da ocorrência de determinados eventos, como:

| Evento                               				| Descrição                                           |
|---------------------------------------------------|-----------------------------------------------------|
|`"account_registry_created"`          				| Criação de uma conta de pagamento.                  |
|`"user_email_verify_email_new_account"` 			| Ativação de um identidade de usuário.               |
|`"user_email_existing_email_new_account"` 			| Aviso de conta já existente.                    	  |
|`"kyc_generic_reject"`                				| Rejeição total de KYC.                              |
|`"kyc_document_photo_unreadable"`     				| Documento ilegivél KYC Pessoa Física.               |
|`"kyc_document_photo_invalid"`        				| Documento inválido KYC Pessoa Física.               |
|`"kyc_social_contract_photos_unreadable"` 			| Documento ilegivél KYC Pessoa Jurídica.             |
|`"kyc_social_contract_photos_invalid"` 			| Documento inválido KYC Pessoa Jurídica.             |
|`"kyc_document_selfies_invalid"`      				| Selfies inválidas KYC.                              |
|`"cash_in_card_payment"`              				| Deposito de um pagamento de crédito.                |
|`"cash_in_payment_refund"`            				| Reembolso de uma pagamento mal sucedido.            |
|`"cash_in_internal_transfer"`         				| Recebimento de uma transferência interna.           |
|`"cash_in_external_transfer"`         				| Recebimento de uma transferência externa.           |
|`"cash_in_external_transfer_refund"`  				| Reembolso de uma transferência externa mal sucedida.|
|`"cash_out_internal_transfer"`        				| Criação de uma transferência interna.               |
|`"cash_out_external_transfer"`        				| Criação de uma transferência externa.               |
|`"cash_out_payment"`                  				| Criação de um pagamento.                            |
|`"cash_out_internal_transfer_failed"` 				| Falha na criação de uma transferência interna.      | 
|`"cash_out_external_transfer_failed"` 				| Falha na criação de uma transferência externa.      |
|`"cash_out_payment_failed"`           				| Falha na criação de um pagamento.                   |
|`"cash_out_internal_transfer_scheduled"` 			| Agendamento de uma transferência interna.           |
|`"cash_out_external_transfer_scheduled"` 			| Agendamento de uma transferência externa.           |
|`"cash_out_payment_scheduled"`        				| Agendamento de um pagamento.                        |
|`"cash_out_internal_transfer_scheduled_failed"` 	| Falha no agendamento de uma transferência interna.  |
|`"cash_out_external_transfer_scheduled_failed"` 	| Falha no agendamento de uma transferência externa.  |
|`"cash_out_payment_scheduled_failed"` 				| Email de notificação um dia antes da transferência interna. |
|`"internal_transfer_day_before_scheduled"` 		| Email de notificação um dia antes da transferência externa. |
|`"external_transfer_day_before_scheduled"` 		| Email de notificação um dia antes do pagamento. |
|`"payment_day_before_scheduled"` 					| Falha no agendamento de um pagamento.        |