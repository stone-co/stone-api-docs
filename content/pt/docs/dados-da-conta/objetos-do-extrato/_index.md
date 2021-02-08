---
title: "Objetos do Extrato"
slug: "objetos-do-extrato"
hidden: false
createdAt: "2020-08-13T18:33:18.658Z"
updatedAt: "2020-10-28T19:48:19.261Z"
weight: 7
---

---
O extrato mostra todos os tipos de transações que ocorreram em determinada conta de pagamento. 

Cada transação é uma nova entrada no extrato e elas estão listadas abaixo com seus campos.

Para ver a estrutura de cada transação, basta dar uma olhadinha aqui do lado ->


### Tipos de Transação

Veja os possíveis valores para o campo `type`, sua descrição e as possíveis combinações com o campo `operation`.

<br>

| Valores type                                   |    Descrição               | Valores Possiveis (Operation)      |
| ---------------------------------------------- | -------------------------  | -----------------------------------|
| balance_blocked                                | Bloqueio de Saldo.         | `credit` ou `debit`  |
| balance_unblocked                              | Desbloqueio de Saldo.      | `credit`
| card_payment                                   | Liquidação de recebíveis de cartão recebido.  | `credit`
| external                                       | Transferência externa. (TED)| `credit` ou `debit`
| external refund                                | Devolução de Transferência externa. | `credit`
| instant_payment                                | Transação de Instant Payment / Qr Code. | `credit` ou `debit` 
| internal                                       | Transferencia interna. | `credit` ou `debit` 
| loan_payments                                  | Valor referente a um empréstimo/crédito | `credit` ou `debit` 
| outbound_stone_prepaid_card_payment            | Compra feita com Cartão Stone. | `debit`
| outbound_stone_prepaid_card_payment_refund     | Devolução de compra com Cartão Stone. | `credit`
| outbound_stone_prepaid_card_payment_chargeback | Devolução do dinheiro a usuária devido ao pedido de chagerback de uma compra feita com cartão Stone.   | `credit`
| outbound_stone_prepaid_card_withdrawal         | Saque com Cartão Stone feito no Banco24Horas. | `debit`
| outbound_stone_prepaid_card_withdrawal_refund  | Devolução de Saque feito no Banco24Horas. | `credit`
| payment                                        | Pagamento de documento com código de barras. | `credit` ou `debit`
| payment refund                                 | Devolução do pagamento de documento com código de barras. | `credit`
| payroll                                        | Folha de pagamento.  | `debit`
| sallary                                        | Recebimento de salário.  | `credit`
| salary_portability                             | Envio do salário para a outra instituição onde foi solicitada a portabilidade. | `debit`
| salary_portability_refund                      | Devolução de salário pela instituição cadastrada na portabilidade. | `credit`
| salary_portability_employer_refund             | Devolução de salário do empregado para a instituição cadastrada na portabilidade. (No caso de processamento do cancelamento da portabilidade, o empregado poderá receber nas duas instituições) | `debit`

---






[block:api-header]
{
  "title": "Tipos de transação"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c3da-4111-98fb-d74f171a31be\",\n         \"amount\":-1000,\n         \"balance_after\":3252,\n         \"balance_before\":4252,\n         \"created_at\":\"2020-08-14T16:15:25Z\",\n         \"id\":\"005d2837-c846-4719-bb17-48f3c40525e4\",\n         \"operation\":\"debit\",\n         \"operation_amount\":1000,\n         \"reason\":\"Saldo bloqueado: Os valores foram bloqueados.Para entender melhor, entre em contato com a gente.\",\n         \"status\":\"FINISHED\",\n         \"type\":\"balance_blocked\"\n      }",
      "language": "json",
      "name": "balance_blocked"
    },
    {
      "code": "\t      {\n        \t\t\"account_id\":\"ad55491e-c1da-4311-98fb-d74f171a31be\",\n        \t\t\"amount\":36900,\n         \t\t\"balance_after\":6035000,\n         \t\t\"balance_before\":5998100,\n         \t\t\"created_at\":\"2020-07-03T15:52:41Z\",\n         \t\t\"id\":\"01fcfd80-e979-4638-9db3-f3217d4cee7e\",\n         \t\t\"operation\":\"credit\",\n        \t\t \"operation_amount\":36900,\n    \t\t\"reason\":\"Saldo bloqueado: Os valores foram bloqueados. Para entender melhor, entre em contato com a gente.\",\n         \t\t\"status\":\"FINISHED\",\n        \t\t\"type\":\"balance_unblocked\"\n      }",
      "language": "json",
      "name": "balance_unblocked"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4111-38fb-d74f171a31be\",\n         \"amount\":-18,\n         \"balance_after\":4252,\n         \"balance_before\":4270,\n         \"counter_party\":{\n            \"account\":{\n               \"account_code\":\"596023\",\n               \"branch_code\":\"1\",\n               \"institution\":\"16501555\",\n               \"institution_name\":\"Stone Pagamentos S.A.\"\n            },\n            \"entity\":{\n               \"name\":\"Nome da Pessoa \"\n            }\n         },\n         \"created_at\":\"2020-08-14T14:11:12Z\",\n         \"description\":\"\",\n         \"fee_amount\":0,\n         \"id\":\"b17e902a-6a10-4ba7-82b7-fd23f8bd80a2\",\n         \"operation\":\"debit\",\n         \"operation_amount\":18,\n         \"operation_id\":\"e2958b86-b3a7-4e8d-9062-16c8feed713d\",\n         \"scheduled_at\":null,\n         \"scheduled_to\":null,\n         \"status\":\"FINISHED\",\n         \"type\":\"internal\"\n      }",
      "language": "json",
      "name": "internal"
    },
    {
      "code": "      {\n         \"account_id\":\"ad55391e-c1da-4111-98fb-d74f171a31be\",\n         \"amount\":-3252,\n         \"balance_after\":0,\n         \"balance_before\":3252,\n         \"counter_party\":{\n            \"account\":{\n               \"account_code\":\"4567864\",\n               \"account_type\":\"CC\",\n               \"branch_code\":\"1234\",\n               \"institution\":\"00000000\",\n               \"institution_name\":\"Banco do Brasil S.A.\"\n            },\n            \"entity\":{\n               \"document\":\"78392364002\",\n               \"document_type\":\"cpf\",\n               \"name\":\"Mell Teste\"\n            }\n         },\n         \"created_at\":\"2020-08-14T18:14:16Z\",\n         \"delayed_to_next_business_day\":false,\n         \"fee_amount\":200,\n         \"id\":\"f8826bd7-dccd-4b90-b0af-e3338b42db61\",\n         \"operation\":\"debit\",\n         \"operation_amount\":3052,\n         \"operation_id\":\"0f09a249-c533-4c6a-a1aa-1a820960a4b1\",\n         \"refund_reason_code\":null,\n         \"refund_reason_description\":null,\n         \"scheduled_at\":null,\n         \"scheduled_to_effective\":null,\n         \"scheduled_to_requested\":null,\n         \"status\":\"FINISHED\",\n         \"type\":\"external\"\n      }",
      "language": "json",
      "name": "external"
    },
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4131-98fb-d74f171a31be\",\n         \"amount\":55,\n         \"balance_after\":6027838,\n         \"balance_before\":6027783,\n         \"counter_party\":{\n            \"account\":{\n               \"account_code\":\"4567864\",\n               \"account_type\":\"CC\",\n               \"branch_code\":\"1234\",\n               \"institution\":\"00000000\",\n               \"institution_name\":\"Banco do Brasil S.A.\"\n            },\n            \"entity\":{\n               \"document\":\"14313050762\",\n               \"document_type\":\"cpf\",\n               \"name\":\"Mell Teste\"\n            }\n         },\n         \"created_at\":\"2020-07-10T16:07:15Z\",\n         \"fee_amount\":0,\n         \"id\":\"65115cdf-6a0e-41d7-37a6-cc4ce5f1bdc3\",\n         \"operation\":\"credit\",\n         \"operation_amount\":55,\n         \"original_operation_id\":\"a16308f5-8c3c-4f8b-8ae4-06e0e1bd0b5c\",\n         \"refund_reason_code\":\"0\",\n         \"refund_reason_description\":\"Ocorreu um erro durante a transferência. Por favor, tente novamente.\",\n         \"refunded_at\":\"2020-07-10T16:07:15Z\",\n         \"status\":\"FINISHED\",\n         \"type\":\"external_refund\"\n      }",
      "language": "json",
      "name": "external_refund"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"amount\":-122,\n         \"balance_after\":1712342,\n         \"balance_before\":1712464,\n         \"counter_party\":{\n            \"entity\":{\n               \"name\":\"Conta Stone\"\n            }\n         },\n         \"created_at\":\"2020-04-01T18:52:37Z\",\n         \"fee_amount\":0,\n         \"id\":\"2355b746-443a-3f14-8f40-ab8b29bd2de8\",\n         \"operation\":\"debit\",\n         \"operation_amount\":122,\n         \"operation_id\":\"f6ecaf2d-636a-4646-9625-ee815ac67b8f\",\n         \"status\":\"FINISHED\",\n         \"type\":\"instant_payment\"\n      }",
      "language": "json",
      "name": "instant_payment"
    },
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4113-98fb-d74f171a31be\",\n         \"acquirer\":\"Stone\",\n         \"amount\":63386,\n         \"balance_after\":64929715,\n         \"balance_before\":64866329,\n         \"card_network_code\":\"VCP\",\n         \"card_network_name\":\"Visa Pré-pago\",\n         \"card_type\":\"debit\",\n         \"created_at\":\"2019-07-10T19:22:01Z\",\n         \"id\":\"72f5e781-01e4-4bc2-8fba-d33f7c67e519\",\n         \"is_prepayment\":true,\n         \"operation\":\"credit\",\n         \"status\":\"FINISHED\",\n         \"type\":\"card_payment\"\n      }",
      "language": "json",
      "name": "card_payment"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4111-98fb-d74f131a31be\",\n         \"amount\":-10000,\n         \"balance_after\":5972000,\n         \"balance_before\":5982000,\n         \"barcode\":\"23791830800000100003381260031315633100006330\",\n         \"created_at\":\"2020-07-03T15:42:36Z\",\n         \"details\":{\n            \"bank_name\":\"BANCO BRADESCO S.A.\",\n            \"discount_value\":0,\n            \"document_payment_type\":null,\n            \"document_type\":\"boleto\",\n            \"expiration_date\":\"2020-07-06\",\n            \"face_value\":null,\n            \"fine_value\":0,\n            \"interest_value\":0,\n            \"max_value\":null,\n            \"min_value\":null,\n            \"payer_cpf_cnpj\":\"96906497000100\",\n            \"payer_legal_name\":\"PAGADOR AMBIENTE HOMOLOGACAO\",\n            \"payer_trade_name\":null,\n            \"payment_end_time\":\"15:00:00\",\n            \"payment_limit_date\":null,\n            \"payment_start_time\":\"07:00:00\",\n            \"recipient_cpf_cnpj\":\"21568259000100\",\n            \"recipient_name\":\"BENEFICIARIO AMBIENTE HOMOLOGACAO\",\n            \"settlement_date\":\"2020-07-03\",\n            \"status\":null,\n            \"total_added_value\":0,\n            \"total_discounted_value\":0,\n            \"updatable_value\":true,\n \"value\":null,\n“writable_line\":\"23793381286003131563371000063306183080000010000\"\n     \t   },\n         \"fee_amount\":0,\n         \"id\":\"631e0e33-0b97-4039-8a0a-255e6b26332d\",\n         \"operation\":\"debit\",\n         \"operation_amount\":10000,\n         \"operation_id\":\"c38fa8a3-5e39-4fff-916d-437c6ff03a44\",\n         \"scheduled_at\":null,\n         \"scheduled_to\":null,\n         \"status\":\"FINISHED\",\n         \"type\":\"payment\",\n       \"writable_line\":\"23793381286003131563371000063306183080000010000\"\n      }",
      "language": "json",
      "name": "payment"
    },
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4111-98fb-d74f131a31be\",\n         \"amount\":15050,\n         \"balance_after\":57387,\n         \"balance_before\":42337,\n         \"barcode\":\"23797807400000140000285090000004630100116850\",\n         \"created_at\":\"2019-11-25T23:34:50Z\",\n         \"details\":{\n            \"bank_name\":\"BANCO BRADESCO S.A.\",\n            \"discount_value\":null,\n            \"document_payment_type\":null,\n            \"document_type\":null,\n            \"expiration_date\":\"2019-11-15\",\n            \"face_value\":null,\n            \"fine_value\":null,\n            \"interest_value\":null,\n            \"max_value\":null,\n            \"min_value\":null,\n            \"payer_cpf_cnpj\":null,\n            \"payer_legal_name\":null,\n            \"payer_trade_name\":null,\n            \"payment_end_time\":null,\n            \"payment_limit_date\":null,\n            \"payment_start_time\":null,\n            \"recipient_cpf_cnpj\":\"21568259000100\",\n            \"recipient_name\":\"BENEFICIARIO AMBIENTE HOMOLOGACAO\",\n            \"settlement_date\":null,\n            \"status\":null,\n            \"total_added_value\":null,\n            \"total_discounted_value\":null,\n            \"updatable_value\":null,\n            \"value\":null,\n    “writable_line\":\"23790285059000000468001001163507780740000014000\"\n         },\n         \"fee_amount\":0,\n         \"id\":\"b7cbd538-f562-46e4-bc27-3dc6fc0c6e15\",\n         \"operation\":\"credit\",\n         \"operation_amount\":15050,\n         \"original_operation_id\":\"4132bfc0-5a38-4ff7-9156-4ba8e7049993\",\n         \"refunded_at\":\"2019-11-25T23:34:50Z\",\n         \"status\":\"FINISHED\",\n         \"type\":\"payment_refund\",\n         \"writable_line\":\"23790285059000000468001001163507780740000014000\"\n      }",
      "language": "json",
      "name": "payment_refund"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"477f8576-ca82-432b-be73-dc28cc6490c3\",\n\"account_settlement_policy_retention\":{\n      \"account_settlement_policy_id\":\"b936a4aa-88e0-4d76-b214-045459e0b7ef\",\n          \"applied_retention_rules\":\n               {\n                  \"acquirer\":null,\n                  \"card_network_code\":null,\n                  \"card_type\":null,\n                  \"desired_rule_amount\":260,\n                  \"effective_rule_amount\":260,\n                  \"is_prepayment\":null,\n                  \"retained_portion\":{\n                     \"coefficient\":1,\n                     \"exponent\":-2\n                      },\n               \"same_ownership\":\"allow\",\n               \"target_account_id\":\"010f38e5-df93-4f0a-bf09-6b28c752c087\"\n               },\n           \"retained_amount\":26098,\n            \"total_amount\":200000\n         },\n         \"amount\":-26098,\n         \"balance_after\":522433099,\n         \"balance_before\":522459197,\n         \"created_at\":\"2020-07-20T18:34:11Z\",\n         \"id\":\"7e289377-f49b-44c7-b301-b63073b734bc\",\n         \"operation\":\"debit\",\n         \"original_operation_entry\":{\n            \"amount\":26099,\n            \"barcode\":\"19791845600000021000003020200528153400979684\",\n            \"barcode_payment_invoice_id\":\"d424397b-331c-47cc-9a9f-0feff6a2c339\",\n            \"beneficiary\":{\n               \"document\":\"91092573062\",\n               \"document_type\":\"cpf\",\n               \"legal_name\":\"Gilderoy  \\\\n \\\\r Lockhart doidaoA\",\n               \"trade_name\":null\n            },\n            \"created_at\":\"2020-07-20T18:34:11Z\",\n            \"invoice_type\":\"deposit\",\n            \"operation\":\"credit\",\n            \"writable_line\":\"19790000052020052815434039796847184560000002100\"\n         },\n         \"original_operation_entry_type\":\"inbound_barcode_payment\",\n         \"status\":\"FINISHED\",\n         \"type\":\"loan_payment\"\n      }",
      "language": "json",
      "name": "loan_payments"
    },
    {
      "code": "     {\n         \"account_id\":\"ad55491e-c1da-4111-93fb-d74f171a31be\",\n         \"amount\":-100,\n         \"balance_after\":5070,\n         \"balance_before\":5170,\n         \"created_at\":\"2020-08-07T18:30:50Z\",\n         \"id\":\"a61fbac3-fcd4-45ee-b47b-e8301d63f668\",\n         \"operation\":\"debit\",\n         \"operation_id\":\"43cdb491-5438-456b-8e8a-2ad801c02933\",\n         \"status\":\"FINISHED\",\n         \"type\":\"payroll\"\n      }",
      "language": "json",
      "name": "payroll"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4111-93fb-d74f171a31be\",\n         \"acquirer_code\":\"acquirer_code\",\n         \"acquirer_name\":null,\n         \"amount\":-149,\n         \"balance_after\":4018,\n         \"balance_before\":4167,\n         \"card_acceptor\":{\n            \"city\":\"my city_2\",\n            \"country\":\"country_4\",\n            \"mcc\":\"mcc_2\",\n            \"name\":\"card_acceptor_name_2\"\n         },\n         \"card_last_four_digits\":\"5851\",\n         \"created_at\":\"2019-12-17T19:00:02Z\",\n         \"fee_amount\":0,\n         \"id\":\"f46e46d6-c569-489a-a0b2-66ef313a3a9a\",\n         \"operation\":\"debit\",\n         \"operation_amount\":149,\n         \"operation_id\":\"5deaa27d-70a1-475d-93c6-1b98cc20229a\",\n         \"status\":\"FINISHED\",\n         \"transaction_authorization\":{\n            \"authorization_medium\":\"authorization_medium_2\",\n            \"captured_value\":{\n              \"amount\":149,\n               \t\"currency\":\"BRL\"\n           \t},\n            \"conversion_rate\":\"1.00\",\n           \t\"country\":\"country_5\",\n           \t\"iof_fee\":null,\n           \t\"pos_authorization_time\":\"2019-12-17T18:32:26\",\n           \t\"value\":{\n           \t    \"amount\":149,\n               \"currency\":\"BRL\"\n       \t     }\n       \t  },\n         \"type\":\"outbound_stone_prepaid_card_payment\"\n      },",
      "language": "json",
      "name": "outbound_stone_prepaid_card_payment"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4111-93fb-d74f171a31be\",\n         \"acquirer_code\":\"acquirer_code\",\n         \"acquirer_name\":null,\n         \"amount\":149,\n         \"balance_after\":3928,\n         \"balance_before\":3779,\n         \"card_acceptor\":{\n            \"city\":\"my city_2\",\n            \"country\":\"country_4\",\n            \"mcc\":\"mcc_2\",\n            \"name\":\"card_acceptor_name_2\"\n         },\n         \"card_last_four_digits\":\"5851\",\n         \"created_at\":\"2019-12-17T19:02:57Z\",\n         \"fee_amount\":0,\n         \"id\":\"6c007930-0206-4a2d-bafd-d2639e5c7fe8\",\n         \"operation\":\"credit\",\n         \"operation_amount\":149,\n         \"operation_id\":\"5deaa27d-70a1-435d-91c6-1b98cc20229a\",\n         \"status\":\"FINISHED\",\n         \"transaction_authorization\":{\n            \"authorization_medium\":\"authorization_medium_2\",\n            \"captured_value\":{\n               \"amount\":149,\n               \"currency\":\"BRL\"\n            },\n            \"conversion_rate\":\"1.00\",\n            \"country\":\"country_5\",\n            \"iof_fee\":null,\n            \"pos_authorization_time\":\"2019-12-17T18:32:26\",\n            \"value\":{\n               \"amount\":149,\n               \"currency\":\"BRL\"\n            }\n         },\n         \"type\":\"outbound_stone_prepaid_card_payment_refund\"\n      }",
      "language": "json",
      "name": "outbound_stone_prepaid_card_payment_refund"
    },
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4111-98fb-d34f171a31be\",\n         \"acquirer_code\":\"acquirer_code\",\n         \"acquirer_name\":null,\n         \"amount\":1,\n         \"balance_after\":4168,\n         \"balance_before\":4167,\n         \"card_acceptor\":{\n            \"city\":\"my city_1\",\n            \"country\":\"country_2\",\n            \"mcc\":\"mcc_1\",\n            \"name\":\"card_acceptor_name_1\"\n         },\n         \"card_last_four_digits\":\"5851\",\n         \"created_at\":\"2019-12-17T20:45:31Z\",\n         \"fee_amount\":0,\n         \"id\":\"11456346-eeab-406c-9cb7-c04366eccd1a\",\n         \"operation\":\"credit\",\n         \"operation_amount\":1,\n         \"operation_id\":\"af2f0286-7338-45b3-ac87-0c7db3ad6b82\",\n         \"status\":\"FINISHED\",\n         \"transaction_authorization\":{\n            \"authorization_medium\":\"authorization_medium_1\",\n            \"captured_value\":{\n               \"amount\":560,\n               \"currency\":\"BRL\"\n            },\n            \"conversion_rate\":\"1.00\",\n            \"country\":\"country_3\",\n            \"iof_fee\":null,\n            \"pos_authorization_time\":\"2019-12-17T18:28:16\",\n            \"value\":{\n               \"amount\":560,\n               \"currency\":\"BRL\"\n            }\n         },\n         \"transaction_chargeback\":{\n            \"charged_back_at\":\"2019-12-17T20:45:31.907317\",\n            \"id\":\"46ab1de4-8e50-4081-98d5-473660d10189\",\n            \"value\":{\n               \"amount\":1,\n               \"currency\":\"BRL\"\n            }\n         },\n         \"type\":\"outbound_stone_prepaid_card_payment_chargeback\"\n      }",
      "language": "json",
      "name": "outbound_stone_prepaid_card_payment_chargeback"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55491e-c1da-4131-98fb-d74f171a31be\",\n         \"acquirer_code\":\"acquirer_code\",\n         \"acquirer_name\":null,\n         \"amount\":-239,\n         \"balance_after\":3779,\n         \"balance_before\":4018,\n         \"card_acceptor\":{\n            \"city\":\"my city_3\",\n            \"country\":\"country_6\",\n            \"mcc\":\"mcc_3\",\n            \"name\":\"card_acceptor_name_3\"\n         },\n         \"card_last_four_digits\":\"5851\",\n         \"created_at\":\"2019-12-17T19:00:03Z\",\n         \"fee_amount\":0,\n         \"id\":\"b56471cf-34de-4305-aba4-de9113388077\",\n         \"operation\":\"debit\",\n         \"operation_amount\":239,\n         \"operation_id\":\"7d6146f8-dd2d-4c93-832d-77215d8c772e\",\n         \"status\":\"REFUNDED\",\n         \"transaction_authorization\":{\n            \"authorization_medium\":\"authorization_medium_3\",\n            \"captured_value\":{\n               \"amount\":239,\n               \"currency\":\"BRL\"\n            },\n            \"conversion_rate\":\"1.00\",\n            \"country\":\"country_7\",\n            \"iof_fee\":null,\n            \"pos_authorization_time\":\"2019-12-17T18:33:14\",\n            \"value\":{\n               \"amount\":239,\n               \"currency\":\"BRL\"\n            }\n         },\n         \"type\":\"outbound_stone_prepaid_card_withdrawal\"\n      }",
      "language": "json",
      "name": "outbound_stone_prepaid_card_withdrawal"
    },
    {
      "code": "    {\n         \"account_id\":\"ad55491e-c1da-4111-38fb-d74f171a31be\",\n         \"acquirer_code\":\"acquirer_code\",\n         \"acquirer_name\":null,\n         \"amount\":239,\n         \"balance_after\":4167,\n         \"balance_before\":3928,\n         \"card_acceptor\":{\n            \"city\":\"my city_3\",\n            \"country\":\"country_6\",\n            \"mcc\":\"mcc_3\",\n            \"name\":\"card_acceptor_name_3\"\n         },\n         \"card_last_four_digits\":\"5851\",\n         \"created_at\":\"2019-12-17T19:02:59Z\",\n         \"fee_amount\":0,\n         \"id\":\"61752b23-96d3-4dab-b0fd-6b8ec2533a11\",\n         \"operation\":\"credit\",\n         \"operation_amount\":239,\n         \"operation_id\":\"7d6146f8-dd2d-4c93-822d-73215d8c772e\",\n         \"status\":\"FINISHED\",\n         \"transaction_authorization\":{\n            \"authorization_medium\":\"authorization_medium_3\",\n            \"captured_value\":{\n               \"amount\":239,\n               \"currency\":\"BRL\"\n            },\n            \"conversion_rate\":\"1.00\",\n            \"country\":\"country_7\",\n            \"iof_fee\":null,\n            \"pos_authorization_time\":\"2019-12-17T18:33:14\",\n            \"value\":{\n               \"amount\":239,\n               \"currency\":\"BRL\"\n            }\n         },\n         \"type\":\"outbound_stone_prepaid_card_withdrawal_refund\"\n      }",
      "language": "json",
      "name": "outbound_stone_prepaid_card_withdrawal_refund"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"ad55391e-c1da-4111-98fb-d74f171a31be\",\n         \"amount\":164,\n         \"balance_after\":39215516,\n         \"balance_before\":39215352,\n         \"counter_party\":{\n            \"account\":{\n               \"account_code\":\"473603\",\n               \"branch_code\":\"1\",\n               \"institution\":\"16501555\",\n               \"institution_name\":\"Stone Pagamentos S.A.\"\n            },\n            \"entity\":{\n               \"document\":\"87939015000106\",\n               \"document_type\":\"cnpj\",\n               \"name\":\"Amazing Corporation S.A.\"\n            }\n         },\n         \"created_at\":\"2019-09-13T22:27:39Z\",\n         \"id\":\"fff5eb35-63bb-44a9-9640-128c97606710\",\n         \"operation\":\"credit\",\n         \"status\":\"FINISHED\",\n         \"type\":\"salary\"\n      },\n",
      "language": "json",
      "name": "salary"
    },
    {
      "code": "      {\n         “account_id”:”ad55431e-c1da-4111-98fb-d74f171a31be” \n         \"amount\":10000,\n         \"balance_after\":5992000,\n         \"balance_before\":5982000,\n         “counter_party”: {\n            \"account\":{\n               \"account_code\":\"473603\",\n               \"branch_code\":\"1\",\n               \"institution\":\"16501555\", \n         \t\t“institution_name”: \"ITAÚ UNIBANCO S.A.\"\n\t}\n         \"created_at\":\"2019-09-13T22:27:39Z\",\n         \"id\":\"fff5eb35-63bb-44a9-9640-128c97606710\",\n         “operation”: \"debit\"\n         “status”: \"FINISHED\"\n         “type”: \"salary_portability\"\n      }",
      "language": "json",
      "name": "salary_portability"
    }
  ],
  "sidebar": true
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "      {\n         \"account_id\":\"477f8576-ca83-462b-be73-dc28cc6490c3\",\n         \"amount\":200,\n         \"balance_after\":522283672,\n         \"balance_before\":522283472,\n         \"counter_party\":{\n            \"account\":{\n               \"account_code\":\"34\",\n               \"branch_code\":\"0001\",\n               \"institution\":\"60746948\",\n               \"institution_name\":\"Banco Bradesco S.A.\"\n            }\n         },\n         \"created_at\":\"2020-06-26T15:33:14Z\",\n         \"id\":\"7270d918-df3d-4a62-8de6-11f3a3b36aa7\",\n         \"operation\":\"credit\",\n         \"refund_reason_code\":\"4\",\n         \"refund_reason_description\":\"Mensagem Inválida para o Tipo de Transação ou Finalidade.\",\n         \"status\":\"FINISHED\",\n         \"type\":\"salary_portability_refund\"\n      }",
      "language": "json",
      "name": "salary_portability_refund"
    },
    {
      "code": "      {\n         \"amount\":-200,\n         \"balance_after\":522283472,\n         \"balance_before\":522283672,\n         \"counter_party\":{\n            \"entity\":{\n               \"document\":\"99999999999\",\n               \"document_type\":\"cpf\",\n               \"name\":\"Nome da Pessoa\"\n            }\n         },\n         \"created_at\":\"2020-06-26T15:33:14Z\",\n         \"id\":\"b9f3722b-9a34-4a89-a94a-9285ba730c50\",\n         \"operation\":\"debit\",\n         \"status\":\"FINISHED\",\n         \"type\":\"salary_portability_employer_refund\"\n      }",
      "language": "json",
      "name": "salary_portability_employer_refund"
    }
  ],
  "sidebar": true
}
[/block]
Veja os possíveis valores para o campo `type`, sua descrição e as possíveis combinações com o campo `operation`.
[block:parameters]
{
  "data": {
    "h-0": "Valores `type`",
    "h-1": "Descrição",
    "h-2": "Valores possiveis `operation`",
    "3-0": "external",
    "3-1": "Transferência externa (TED).",
    "6-0": "internal",
    "6-1": "Transferencia interna.",
    "13-0": "payment",
    "13-1": "Pagamento de documento com código de barras.",
    "3-2": "`credit` ou `debit`",
    "6-2": "`credit` ou `debit`",
    "13-2": "`credit` ou `debit`",
    "4-0": "external refund",
    "4-2": "`credit`",
    "4-1": "Devolução de transferência externa.",
    "14-0": "payment refund",
    "14-1": "Devolução do pagamento de documento com código de barras.",
    "14-2": "`credit`",
    "2-0": "card_payment",
    "2-1": "Liquidação de recebíveis de cartão recebida.",
    "2-2": "`credit`",
    "0-0": "balance_blocked",
    "0-1": "Bloqueio de saldo.",
    "0-2": "`credit` ou `debit`",
    "1-0": "balance_unblocked",
    "1-1": "Desbloqueio de saldo.",
    "1-2": "`credit`",
    "15-0": "payroll",
    "15-1": "Folha de pagamento.",
    "15-2": "`debit`",
    "16-0": "sallary",
    "16-1": "Recebimento de salário.",
    "16-2": "`credit`",
    "17-0": "salary_portability",
    "17-2": "`debit`",
    "17-1": "Envio do salário para a outra instituição onde foi solicitada a portabilidade.",
    "18-0": "salary_portability_refund",
    "18-1": "Devolução de salário pela instituição cadastrada na portabilidade.",
    "18-2": "`credit`",
    "19-0": "salary_portability_employer_refund",
    "19-1": "Devolução de salário do empregado para a instituição cadastrada na portabilidade. (No caso de processamento do cancelamento da portabilidade, o empregado poderá receber nas duas instituições)",
    "19-2": "`debit`",
    "11-0": "outbound_stone_prepaid_card_withdrawal",
    "8-0": "outbound_stone_prepaid_card_payment",
    "9-0": "outbound_stone_prepaid_card_payment_refund",
    "10-0": "outbound_stone_prepaid_card_payment_chargeback",
    "12-0": "outbound_stone_prepaid_card_withdrawal_refund",
    "12-1": "Devolução de Saque feito no Banco24Horas",
    "12-2": "`credit`",
    "11-1": "Saque com Cartão Stone feito no Banco24Horas.",
    "11-2": "`debit`",
    "10-1": "Devolução do dinheiro a usuária devido ao pedido de chagerback de uma compra feita com cartão Stone.",
    "10-2": "`credit`",
    "9-1": "Devolução de compra com Cartão Stone.",
    "9-2": "`credit`",
    "8-1": "Compra feita com Cartão Stone.",
    "8-2": "`debit`",
    "5-0": "instant_payment",
    "5-2": "`credit` ou `debit`",
    "5-1": "Transação de Instant Payment / Qr Code.",
    "7-0": "loan_payments",
    "7-2": "`credit` ou `debit`",
    "7-1": "Valor referente a um empréstimo/crédito."
  },
  "cols": 3,
  "rows": 20
}
[/block]

[block:api-header]
{
  "title": "Campos das transações"
}
[/block]
Todas as entradas do extrato tem alguns campos padrões são eles:
[block:parameters]
{
  "data": {
    "0-0": "type",
    "1-0": "operation",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-2": "*String* ",
    "0-1": "Identifica o tipo de movimentação do extrato. Veja os possíveis valores desse campo na tabela [acima](ref:objetos-do-extrato)",
    "1-1": "Identifica se a movimentação foi de entrada de dinheiro, `credit`, ou de saída de dinheiro `debit`. Veja as combinações possíveis de tipos e operações na tabela  [acima](ref:objetos-do-extrato).",
    "1-2": "*String* ",
    "2-0": "balance_before",
    "4-0": "amount",
    "3-0": "balance_after",
    "5-0": "account_id",
    "5-1": "ID da conta pagamento a qual essa entrada pertence.",
    "5-2": "*String*",
    "2-1": "Saldo antes da operação ocorrer.",
    "2-2": "*Integer*",
    "3-2": "*Integer*",
    "4-2": "*Integer*",
    "3-1": "Saldo disponível após o valor da operação, incluindo taxas.",
    "4-1": "Valor da operação sem taxas.",
    "6-0": "created_at",
    "7-0": "status",
    "6-1": "Data de processamento da transação / de entrada da transação no extrato. Formato: datetime.",
    "6-2": "*String*",
    "7-1": "Status atual da transação. Varia de acordo com o tipo de transação.",
    "7-2": "*String*",
    "8-0": "id",
    "8-1": "Identificador da transação que originou essa movimentação no extrato",
    "8-2": "*String*"
  },
  "cols": 3,
  "rows": 9
}
[/block]
Abaixo temos os campos que são utilizados em cada tipo de transação no extrato:
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "operation_amount",
    "1-0": "reason",
    "0-1": "Valor bloqueado ou desbloqueado na operação.",
    "1-1": "Motivo do bloqueio ou desbloqueio.",
    "0-3": "`balance_blocked`, `balance_unblocked`)",
    "1-3": "`balance_blocked`, `balance_unblocked`",
    "2-0": "acquirer",
    "3-0": "card_network_code",
    "4-0": "card_network_name",
    "5-0": "card_type",
    "6-0": "is_prepayment",
    "2-3": "`card_payment`",
    "3-3": "`card_payment`",
    "4-3": "`card_payment`",
    "5-3": "`card_payment`",
    "6-3": "`card_payment`",
    "2-2": "*String*",
    "3-2": "*String*",
    "0-2": "*String*",
    "1-2": "*String*",
    "4-2": "*String*",
    "5-2": "*String*",
    "6-2": "*Boolean*",
    "7-0": "counter_party",
    "7-2": "*Object*",
    "7-1": "Dados do beneficiário da transação. Veja os campos desse objeto abaixo.",
    "7-3": "`external`, `external_refund`, `instant_payment`, `internal`, `salary`, `salary_portability`, `salary_portability_refund`, `salary_portability_employer_refund`",
    "h-3": "Transação",
    "8-0": "delayed_to_next_business_day",
    "8-3": "`external`",
    "8-2": "*Boolean*",
    "9-0": "fee_amount",
    "9-3": "`external`, `external_refund`, \n`instant_payment`, `internal`, `outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`, `payment`, `payment_refund`",
    "9-2": "*Integer*",
    "10-0": "operation_amount",
    "10-2": "*Integer*",
    "10-3": "`external`, `external_refund`, `instant_payment`, `internal`, `outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`, `payment`, `payment_refund`",
    "11-0": "operation_id",
    "11-2": "*String*",
    "11-3": "`external`, `instant_payment`, `internal`, `outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`, `payment`, `payroll`",
    "12-0": "refund_reason_code",
    "13-0": "refund_reason_description",
    "14-0": "scheduled_at",
    "15-0": "scheduled_to_effective",
    "16-0": "scheduled_to_requested",
    "12-3": "`external`, `external_refund`, `salary_portability_refund`",
    "13-3": "`external`, `external_refund`, `salary_portability_refund`",
    "14-3": "`external`, `internal`, `payment`",
    "15-3": "`external`",
    "16-3": "`external`",
    "12-2": "*String*",
    "13-2": "*String*",
    "14-2": "*String*",
    "15-2": "*String*",
    "16-2": "*String*",
    "17-0": "original_operation_id",
    "17-2": "*String*",
    "17-3": "`external_refund`, `payment_refund`",
    "18-0": "refunded_at",
    "18-2": "*String*",
    "18-3": "`external_refund`, `payment_refund`",
    "19-3": "`internal`",
    "19-0": "schedule_to",
    "19-2": "*String*",
    "20-3": "`loan_payments`",
    "20-0": "account_settlement_policy_retention",
    "20-2": "*Object*",
    "21-0": "original_operation_entry",
    "21-2": "*Object*",
    "21-3": "`loan_payments`",
    "22-0": "original_operation_entry_type",
    "22-3": "`loan_payments`",
    "22-2": "*String*",
    "23-0": "acquirer_code",
    "24-0": "acquirer_name",
    "23-2": "*String*",
    "24-2": "*String*",
    "23-3": "`outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`",
    "24-3": "`outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`",
    "25-0": "card_acceptor",
    "25-2": "*Object*",
    "25-3": "`outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`",
    "26-0": "card_last_four_digits",
    "26-2": "*String*",
    "26-3": "`outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`",
    "27-0": "transaction_authorization",
    "27-2": "*Object*",
    "27-3": "`outbound_stone_prepaid_card_payment`, `outbound_stone_prepaid_card_payment_refund`, `outbound_stone_prepaid_card_payment_chargeback`, `outbound_stone_prepaid_card_withdrawal`, `outbound_stone_prepaid_card_withdrawal_refund`",
    "28-3": "`outbound_stone_prepaid_card_payment_chargeback`",
    "28-0": "transaction_chargeback",
    "28-2": "*Object*",
    "29-3": "`payment`",
    "29-0": "barcode",
    "29-2": "*String*",
    "30-0": "details",
    "30-2": "*Object*",
    "30-3": "`payment`, `payment_refund`",
    "31-3": "`payment`",
    "32-3": "`payment`, `payment_refund`",
    "31-0": "scheduled_to",
    "32-0": "writable_line",
    "31-2": "*String*",
    "32-2": "*String*",
    "2-1": "Instituição responsável pela liquidação de recebíveis.",
    "3-1": "Código da rede do cartão.",
    "4-1": "Nome da rede do cartão.",
    "5-1": "Tipo do cartão.",
    "6-1": "Informa se o cartão é do tipo pré-pago ou não.",
    "8-1": "Informa se a transação foi adiada para o próximo dia útil ou não.",
    "9-1": "Valor da taxa da transação.",
    "10-1": "Valor da operação, sem o valor da taxa.",
    "11-1": "Código identificador da operação.",
    "12-1": "Código da razão da devolução da transação.",
    "13-1": "Descrição da razão de devolução da transação.",
    "14-1": "Data em que foi realizado o agendamento da transação.",
    "15-1": "Data que o sistema agendou para realizar a transação.",
    "16-1": "Data solicitada para agendamento da transação.",
    "17-1": "Código identificador da operação original.",
    "18-1": "Data em que a transação foi devolvida.",
    "19-1": "Data para qual foi realizado o agendamento da transação.",
    "20-1": "Dados da conta em que será realizada a retenção de liquidação de conta",
    "21-1": "Dados da operação original.",
    "22-1": "Tipo da operação original.",
    "23-1": "Código do adquirente.",
    "24-1": "Nome do adquirente",
    "25-1": "Dados sobre o cartão em que foi realizada a compra.",
    "26-1": "Últimos dígitos do cartão em que foi realizada a compra.",
    "27-1": "Dados sobre a autorização da transação de uma compra feita com cartão..",
    "28-1": "Dados sobre o estorno da transação de uma compra feita com cartão.\nVeja os campos desse objeto",
    "29-1": "Código de barras de um boleto.",
    "30-1": "Dados sobre o pagamento de um boleto.\nVeja mais sobre esse campo [aqui](https://docs.openbank.stone.com.br/reference#objetos-simulação-de-pagamento)",
    "31-1": "Data para qual foi agendado o pagamento de um boleto.",
    "32-1": "Linha digitável de um boleto."
  },
  "cols": 4,
  "rows": 33
}
[/block]
## Campos do objeto `counter_party`: 
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "account",
    "0-2": "*Object*",
    "1-0": "entity",
    "1-2": "*Object*",
    "0-1": "Dados da conta destino.",
    "1-1": "Dados pessoais."
  },
  "cols": 3,
  "rows": 2
}
[/block]
Campos do objeto `account`:
[block:parameters]
{
  "data": {
    "0-0": "account_code",
    "1-0": "account_type",
    "2-0": "branch_code",
    "3-0": "institution",
    "4-0": "institution_name",
    "0-2": "*Integer*",
    "2-2": "*Integer*",
    "3-2": "*Integer*",
    "4-2": "*String*",
    "1-2": "*String*",
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-1": "Código da conta.",
    "1-1": "Tipo da conta.",
    "2-1": "Agência da conta.",
    "3-1": "Código da instituição da conta.",
    "4-1": "Nome da instituição da conta."
  },
  "cols": 3,
  "rows": 5
}
[/block]
Campos do objeto `entity`:
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "document",
    "1-0": "document_type",
    "2-0": "name",
    "0-2": "*Integer*",
    "1-2": "*String*",
    "2-2": "*String*",
    "0-1": "Número de documento do responsável da conta.",
    "1-1": "Tipo de documento do responsável da conta.",
    "2-1": "Nome  do responsável da conta."
  },
  "cols": 3,
  "rows": 3
}
[/block]
Campos do objeto `account_settlement_policy_retention`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "account_settlement_policy_id",
    "1-0": "applied_retention_rules",
    "2-0": "retained_amount",
    "3-0": "total_amount",
    "1-2": "*Object*",
    "0-2": "*String*",
    "2-2": "*Integer*",
    "3-2": "*Integer*",
    "0-1": "Identificador único dos juros do empréstimo/crédito.",
    "1-1": "Dados de onde será aplicada as regras de juros.",
    "2-1": "Valor dos juros.",
    "3-1": "Valor total do empréstimo/crédito."
  },
  "cols": 3,
  "rows": 4
}
[/block]
Campos do objeto `applied_retention_rules` 
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "acquirer",
    "1-0": "card_network_code",
    "2-0": "card_type",
    "3-0": "desired_rule_amount",
    "4-0": "effective_rule_amount",
    "5-0": "is_prepayment",
    "6-0": "retained_portion",
    "7-0": "same_ownership",
    "8-0": "target_account_id",
    "6-2": "*Object*",
    "0-2": "*String*",
    "1-2": "*String*",
    "2-2": "*String*",
    "3-2": "*Integer*",
    "4-2": "*Integer*",
    "5-2": "*Boolean*",
    "7-2": "*String*",
    "8-2": "*String*",
    "0-1": "Instituição responsável pela liquidação de recebíveis.",
    "1-1": "Código da rede do cartão.",
    "2-1": "Tipo de cartão",
    "3-1": "Valor desejado do juros.",
    "4-1": "Valor efetivo dos juros.",
    "5-1": "Informa se o cartão é do tipo  pré-pago ou não.",
    "6-1": "Dados sobre a porcentagem dos juros.",
    "7-1": "Informa se o pagador pode ser da mesma instituição que o beneficiário.",
    "8-1": "Identificador da conta que ira receber o empréstimo/crédito."
  },
  "cols": 3,
  "rows": 9
}
[/block]
Campos do objeto `retained_portion`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "coefficient",
    "1-0": "exponent",
    "0-2": "*Integer*",
    "1-2": "*Integer*",
    "0-1": "Valor do coeficiente para cálculo dos juros do empréstimo/crédito.",
    "1-1": "Valor do expoente para cálculo dos juros do empréstimo/crédito."
  },
  "cols": 3,
  "rows": 2
}
[/block]
Campos do objeto `original_operation_entry`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "amount",
    "1-0": "barcode",
    "2-0": "barcode_payment_invoice_id",
    "3-0": "beneficiary",
    "4-0": "created_at",
    "5-0": "invoice_type",
    "6-0": "operation",
    "7-0": "writable_line",
    "3-2": "*Object*",
    "0-2": "*Integer*",
    "1-2": "*String*",
    "2-2": "*String*",
    "4-2": "*String*",
    "5-2": "*String*",
    "6-2": "*String*",
    "7-2": "*String*",
    "0-1": "Valor original retido para pagamento do empréstimo/crédito.",
    "1-1": "Código de barras referente ao empréstimo/crédito.",
    "2-1": "Identificador do pagamento do código de barras do empréstimo/crédito.",
    "3-1": "Dados do beneficário do empréstimo/crédito.",
    "4-1": "Data da criação do pedido do empréstimo/crédito.",
    "5-1": "Tipo de fatura do empréstimo/crédito.",
    "6-1": "Tipo de operação do empréstimo/crédito.",
    "7-1": "Linha digitável do empréstimo/crédito."
  },
  "cols": 3,
  "rows": 8
}
[/block]
Campos do objeto `beneficiary`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "document",
    "1-0": "document_type",
    "2-0": "legal_name",
    "3-0": "trade_name",
    "0-2": "*String*",
    "1-2": "*String*",
    "2-2": "*String*",
    "3-2": "*String*",
    "0-1": "Documento do beneficiário.",
    "1-1": "Tipo do documento do beneficiário.",
    "2-1": "Nome completo ou razão social do beneficiário.",
    "3-1": "Nome fantasia do beneficiário. Campo não obrigatório."
  },
  "cols": 3,
  "rows": 4
}
[/block]
Campos do objeto `card_acceptor`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "city",
    "1-0": "country",
    "2-0": "mcc",
    "3-0": "name",
    "0-2": "*String*",
    "1-2": "*String*",
    "2-2": "*String*",
    "3-2": "*String*",
    "0-1": "Cidade onde foi realizada a compra.",
    "1-1": "País onde foi realizada a compra.",
    "3-1": "Nome do dono do cartão.",
    "2-1": "Tipo de taxa que será aplicada à compra. (Ex.: taxa de intercâmbio, taxa da rede do cartão, entre outras)"
  },
  "cols": 3,
  "rows": 4
}
[/block]
Campos do objeto `transaction_authorization`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "authorization_medium",
    "1-0": "captured_value",
    "1-2": "*Object*",
    "2-0": "conversion_rate",
    "3-0": "country",
    "4-0": "iof_fee",
    "5-0": "pos_authorization_time",
    "6-0": "value",
    "6-2": "*Object*",
    "0-2": "*String*",
    "2-2": "*String*",
    "3-2": "*String*",
    "5-2": "*String*",
    "4-2": "*Integer*",
    "0-1": "Tipo de autorização recebida na compra.",
    "1-1": "Dados do valor na moeda em que ocorreu a compra, sem taxas",
    "2-1": "Taxa de conversão.",
    "3-1": "Código do país onde ocorreu a compra.",
    "4-1": "Taxa de IOF. Campo não obrigatório.",
    "5-1": "Data da autorização.",
    "6-1": "Dados do valor convertido pra BRL, com taxas."
  },
  "cols": 3,
  "rows": 7
}
[/block]
Campos do objeto `captured_value`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "amount",
    "1-0": "currency",
    "1-2": "*String*",
    "0-2": "*Integer*",
    "0-1": "Valor capturado no momento da compra via cartão, sem taxas.",
    "1-1": "Moeda utilizada no momento da compra via cartão."
  },
  "cols": 3,
  "rows": 2
}
[/block]
Campos do objeto `value`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "amount",
    "1-0": "currency",
    "0-2": "*Integer*",
    "1-2": "*String*",
    "1-1": "Moeda convertida para BRL.",
    "0-1": "Valor total da compra convertido para BRL, com taxas incluídas."
  },
  "cols": 3,
  "rows": 2
}
[/block]
Campos do objeto `transaction_chargeback`
[block:parameters]
{
  "data": {
    "h-0": "Chave",
    "h-1": "Descrição",
    "h-2": "Tipo",
    "0-0": "charged_back_at",
    "1-0": "id",
    "2-0": "value",
    "2-2": "*Object*",
    "1-2": "*String*",
    "0-2": "*String*",
    "0-1": "Data em que ocorreu a devolução do valor da compra.",
    "1-1": "Identificador da devolução da transação.",
    "2-1": "Dados do valor estornado."
  },
  "cols": 3,
  "rows": 3
}
[/block]