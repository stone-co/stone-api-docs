---
title: "Estrutura de Transações no Extrato"
slug: "estrutura-de-transacoes-no-extrato"
createdAt: "2021-02-12T16:10:18.658Z"
weight: 1
---

---
Veja as possíveis estruturas de cada transação que poderão imapactar o extrato.

<br>

---
##### Saldo bloqueado 

```JSON
{
	"balance_blocked": {
		"account_id": "ad55491e-c3da-4111-98fb-d74f171a31be",
		"amount": -1000,
		"balance_after": 3252,
		"balance_before": 4252,
		"created_at": "2020-08-14T16:15:25Z",
		"id": "005d2837-c846-4719-bb17-48f3c40525e4",
		"operation": "debit",
		"operation_amount": 1000,
		"reason": "Saldo bloqueado: Os valores foram bloqueados.Para entender melhor, entre em contato com a gente.",
		"status": "FINISHED",
		"type": "balance_blocked"
	}
}
```

##### Saldo desbloqueado 

```JSON
{
	"balance_unblocked": {            
		"account_id":"ad55491e-c1da-4311-98fb-d74f171a31be",
		"amount":36900,
		"balance_after":6035000,
		"balance_before":5998100,
		"created_at":"2020-07-03T15:52:41Z",
		"id":"01fcfd80-e979-4638-9db3-f3217d4cee7e",
		"operation":"credit",
		"operation_amount":36900,
		"reason":"Saldo bloqueado: Os valores foram bloqueados. Para entender melhor, entre em contato com a gente.",
		"status":"FINISHED",
		"type":"balance_unblocked"
	}
}

```
##### Transferência interna

```JSON
{
	"internal": {
		"account_id":"ad55491e-c1da-4111-38fb-d74f171a31be",
         "amount":-18,
         "balance_after":4252,
         "balance_before":4270,
         "counter_party":{
            "account":{
               "account_code":"596023",
               "branch_code":"1",
               "institution":"16501555",
               "institution_name":"Stone Pagamentos S.A."
            },
            "entity":{
               "name":"Nome da Pessoa "
            }
         },
         "created_at":"2020-08-14T14:11:12Z",
         "description":"",
         "fee_amount":0,
         "id":"b17e902a-6a10-4ba7-82b7-fd23f8bd80a2",
         "operation":"debit",
         "operation_amount":18,
         "operation_id":"e2958b86-b3a7-4e8d-9062-16c8feed713d",
         "scheduled_at":null,
         "scheduled_to":null,
         "status":"FINISHED",
         "type":"internal"
	}
}
```
##### Transferência externa

```JSON
{
	"external": {            
		"account_id":"ad55391e-c1da-4111-98fb-d74f171a31be",
         "amount":-3252,
         "balance_after":0,
         "balance_before":3252,
         "counter_party":{
            "account":{
               "account_code":"4567864",
               "account_type":"CC",
               "branch_code":"1234",
               "institution":"00000000",
               "institution_name":"Banco do Brasil S.A."
            },
            "entity":{
               "document":"78392364002",
               "document_type":"cpf",
               "name":"Mell Teste"
            }
         },
         "created_at":"2020-08-14T18:14:16Z",
         "delayed_to_next_business_day":false,
         "fee_amount":200,
         "id":"f8826bd7-dccd-4b90-b0af-e3338b42db61",
         "operation":"debit",
         "operation_amount":3052,
         "operation_id":"0f09a249-c533-4c6a-a1aa-1a820960a4b1",
         "refund_reason_code":null,
         "refund_reason_description":null,
         "scheduled_at":null,
         "scheduled_to_effective":null,
         "scheduled_to_requested":null,
         "status":"FINISHED",
         "type":"external"
	}
}
```
##### Devolução de transferência externa

```JSON
{
	"external_refund": {            
		"account_id":"ad55491e-c1da-4131-98fb-d74f171a31be",
         "amount":55,
         "balance_after":6027838,
         "balance_before":6027783,
         "counter_party":{
            "account":{
               "account_code":"4567864",
               "account_type":"CC",
               "branch_code":"1234",
               "institution":"00000000",
               "institution_name":"Banco do Brasil S.A."
            },
            "entity":{
               "document":"14313050762",
               "document_type":"cpf",
               "name":"Mell Teste"
            }
         },
         "created_at":"2020-07-10T16:07:15Z",
         "fee_amount":0,
         "id":"65115cdf-6a0e-41d7-37a6-cc4ce5f1bdc3",
         "operation":"credit",
         "operation_amount":55,
         "original_operation_id":"a16308f5-8c3c-4f8b-8ae4-06e0e1bd0b5c",
         "refund_reason_code":"0",
         "refund_reason_description":"Ocorreu um erro durante a transferência. Por favor, tente novamente.",
         "refunded_at":"2020-07-10T16:07:15Z",
         "status":"FINISHED",
         "type":"external_refund"
	}
}

```
##### Pagamento instantâneo

```JSON
{
	"instant_payment": {
		"amount":-122,
         "balance_after":1712342,
         "balance_before":1712464,
         "counter_party":{
            "entity":{
               "name":"Conta Stone"
            }
         },
         "created_at":"2020-04-01T18:52:37Z",
         "fee_amount":0,
         "id":"2355b746-443a-3f14-8f40-ab8b29bd2de8",
         "operation":"debit",
         "operation_amount":122,
         "operation_id":"f6ecaf2d-636a-4646-9625-ee815ac67b8f",
         "status":"FINISHED",
         "type":"instant_payment"
	}
}
```
##### Liquidação de recebíveis de cartão

```JSON
{
	"card_payment": {            
		"account_id":"ad55491e-c1da-4113-98fb-d74f171a31be",
         "acquirer":"Stone",
         "amount":63386,
         "balance_after":64929715,
         "balance_before":64866329,
         "card_network_code":"VCP",
         "card_network_name":"Visa Pré-pago",
         "card_type":"debit",
         "created_at":"2019-07-10T19:22:01Z",
         "id":"72f5e781-01e4-4bc2-8fba-d33f7c67e519",
         "is_prepayment":true,
         "operation":"credit",
         "status":"FINISHED",
         "type":"card_payment"
	}	
}

```
##### Pagamento de boleto

```JSON
{
	"payment": {
		 "account_id":"ad55491e-c1da-4111-98fb-d74f131a31be",
         "amount":-10000,
         "balance_after":5972000,
         "balance_before":5982000,
         "barcode":"23791830800000100003381260031315633100006330",
         "created_at":"2020-07-03T15:42:36Z",
         "details":{
            "bank_name":"BANCO BRADESCO S.A.",
            "discount_value":0,
            "document_payment_type":null,
            "document_type":"boleto",
            "expiration_date":"2020-07-06",
            "face_value":null,
            "fine_value":0,
            "interest_value":0,
            "max_value":null,
            "min_value":null,
            "payer_cpf_cnpj":"96906497000100",
            "payer_legal_name":"PAGADOR AMBIENTE HOMOLOGACAO",
            "payer_trade_name":null,
            "payment_end_time":"15:00:00",
            "payment_limit_date":null,
            "payment_start_time":"07:00:00",
            "recipient_cpf_cnpj":"21568259000100",
            "recipient_name":"BENEFICIARIO AMBIENTE HOMOLOGACAO",
            "settlement_date":"2020-07-03",
            "status":null,
            "total_added_value":0,
            "total_discounted_value":0,
            "updatable_value":true,
 			"value":null,
			"writable_line":"23793381286003131563371000063306183080000010000"
           },
			"fee_amount":0,
			"id":"631e0e33-0b97-4039-8a0a-255e6b26332d",
			"operation":"debit",
			"operation_amount":10000,
			"operation_id":"c38fa8a3-5e39-4fff-916d-437c6ff03a44",
			"scheduled_at":null,
			"scheduled_to":null,
			"status":"FINISHED",
			"type":"payment",
       		"writable_line":"23793381286003131563371000063306183080000010000"
	}
}
```
##### Devolução de pagamento

```JSON
{
	"payment_refund": {            
		"account_id":"ad55491e-c1da-4111-98fb-d74f131a31be",
         "amount":15050,
         "balance_after":57387,
         "balance_before":42337,
         "barcode":"23797807400000140000285090000004630100116850",
         "created_at":"2019-11-25T23:34:50Z",
         "details":{
            "bank_name":"BANCO BRADESCO S.A.",
            "discount_value":null,
            "document_payment_type":null,
            "document_type":null,
            "expiration_date":"2019-11-15",
            "face_value":null,
            "fine_value":null,
            "interest_value":null,
            "max_value":null,
            "min_value":null,
            "payer_cpf_cnpj":null,
            "payer_legal_name":null,
            "payer_trade_name":null,
            "payment_end_time":null,
            "payment_limit_date":null,
            "payment_start_time":null,
            "recipient_cpf_cnpj":"21568259000100",
            "recipient_name":"BENEFICIARIO AMBIENTE HOMOLOGACAO",
            "settlement_date":null,
            "status":null,
            "total_added_value":null,
            "total_discounted_value":null,
            "updatable_value":null,
            "value":null,
			"writable_line":"23790285059000000468001001163507780740000014000"
         },
         "fee_amount":0,
         "id":"b7cbd538-f562-46e4-bc27-3dc6fc0c6e15",
         "operation":"credit",
         "operation_amount":15050,
         "original_operation_id":"4132bfc0-5a38-4ff7-9156-4ba8e7049993",
         "refunded_at":"2019-11-25T23:34:50Z",
         "status":"FINISHED",
         "type":"payment_refund",
         "writable_line":"23790285059000000468001001163507780740000014000"
    }	
}

```

##### Empréstimos 

```JSON
{
	"loan_payments": {
		"account_id":"477f8576-ca82-432b-be73-dc28cc6490c3",
		"account_settlement_policy_retention":{
			"account_settlement_policy_id":"b936a4aa-88e0-4d76-b214-045459e0b7ef",
			"applied_retention_rules":{
					"acquirer":null,
					"card_network_code":null,
					"card_type":null,
					"desired_rule_amount":260,
					"effective_rule_amount":260,
					"is_prepayment":null,
					"retained_portion":{
						"coefficient":1,
						"exponent":-2
                    },
               		"same_ownership":"allow",
					"target_account_id":"010f38e5-df93-4f0a-bf09-6b28c752c087"
			},
			"retained_amount":26098,
			"total_amount":200000
        },
        "amount":-26098,
        "balance_after":522433099,
        "balance_before":522459197,
        "created_at":"2020-07-20T18:34:11Z",
        "id":"7e289377-f49b-44c7-b301-b63073b734bc",
        "operation":"debit",
        "original_operation_entry":{
			"amount":26099,
            "barcode":"19791845600000021000003020200528153400979684",
			"barcode_payment_invoice_id":"d424397b-331c-47cc-9a9f-0feff6a2c339",
            "beneficiary":{
               "document":"91092573062",
               "document_type":"cpf",
               "legal_name":"Gilderoy  \\n \\r Lockhart doidaoA",
               "trade_name":null
            },
            "created_at":"2020-07-20T18:34:11Z",
            "invoice_type":"deposit",
            "operation":"credit",  
			"writable_line":"19790000052020052815434039796847184560000002100"
        },
        "original_operation_entry_type":"inbound_barcode_payment",
        "status":"FINISHED",
        "type":"loan_payment"
	}
}
	
```

##### Folha de Pagamento 

```JSON
{
	"payroll": {            
		"account_id":"ad55491e-c1da-4111-93fb-d74f171a31be",
         "amount":-100,
         "balance_after":5070,
         "balance_before":5170,
         "created_at":"2020-08-07T18:30:50Z",
         "id":"a61fbac3-fcd4-45ee-b47b-e8301d63f668",
         "operation":"debit",
         "operation_id":"43cdb491-5438-456b-8e8a-2ad801c02933",
         "status":"FINISHED",
         "type":"payroll"
    }	
}

```

##### Compra feita com Cartão Stone 

```JSON
{	
	"outbound_stone_prepaid_card_payment": {            
		"account_id":"ad55491e-c1da-4111-93fb-d74f171a31be",
        "acquirer_code":"acquirer_code",
        "acquirer_name":null,
        "amount":-149,
        "balance_after":4018,
        "balance_before":4167,
        "card_acceptor":{
            "city":"my city_2",
            "country":"country_4",
            "mcc":"mcc_2",
            "name":"card_acceptor_name_2"
        },
        "card_last_four_digits":"5851",
        "created_at":"2019-12-17T19:00:02Z",
        "fee_amount":0,
        "id":"f46e46d6-c569-489a-a0b2-66ef313a3a9a",
        "operation":"debit",
        "operation_amount":149,
        "operation_id":"5deaa27d-70a1-475d-93c6-1b98cc20229a",
        "status":"FINISHED",
        "transaction_authorization":{
            "authorization_medium":"authorization_medium_2",
            "captured_value":{
				"amount":149,
                "currency":"BRL"
            },
            "conversion_rate":"1.00",
            "country":"country_5",
            "iof_fee":null,
            "pos_authorization_time":"2019-12-17T18:32:26",
            "value":{
				"amount":149,
				"currency":"BRL"
            }
        },
        "type":"outbound_stone_prepaid_card_payment"
    }	
}

```

##### Devolução de compra feita com Cartão Stone 

```JSON 
{
	"outbound_stone_prepaid_card_payment_refund": {
		"account_id":"ad55491e-c1da-4111-93fb-d74f171a31be",
        "acquirer_code":"acquirer_code",
        "acquirer_name":null,
        "amount":149,
        "balance_after":3928,
        "balance_before":3779,
        "card_acceptor":{
            "city":"my city_2",
            "country":"country_4",
            "mcc":"mcc_2",
            "name":"card_acceptor_name_2"
        },
        "card_last_four_digits":"5851",
        "created_at":"2019-12-17T19:02:57Z",
        "fee_amount":0,
        "id":"6c007930-0206-4a2d-bafd-d2639e5c7fe8",
        "operation":"credit",
        "operation_amount":149,
        "operation_id":"5deaa27d-70a1-435d-91c6-1b98cc20229a",
        "status":"FINISHED",
        "transaction_authorization":{
            "authorization_medium":"authorization_medium_2",
            "captured_value":{
               "amount":149,
               "currency":"BRL"
            },
            "conversion_rate":"1.00",
            "country":"country_5",
            "iof_fee":null,
            "pos_authorization_time":"2019-12-17T18:32:26",
            "value":{
               "amount":149,
               "currency":"BRL"
            }
        },
        "type":"outbound_stone_prepaid_card_payment_refund"
	}
}
	
```

##### Chargeback de uma compra feita com Cartão Stone

```JSON
{
	"outbound_stone_prepaid_card_payment_chargeback": {            
		 "account_id":"ad55491e-c1da-4111-98fb-d34f171a31be",
         "acquirer_code":"acquirer_code",
         "acquirer_name":null,
         "amount":1,
         "balance_after":4168,
         "balance_before":4167,
        "card_acceptor":{
            "city":"my city_1",
            "country":"country_2",
            "mcc":"mcc_1",
            "name":"card_acceptor_name_1"
        },
         "card_last_four_digits":"5851",
         "created_at":"2019-12-17T20:45:31Z",
         "fee_amount":0,
         "id":"11456346-eeab-406c-9cb7-c04366eccd1a",
         "operation":"credit",
         "operation_amount":1,
         "operation_id":"af2f0286-7338-45b3-ac87-0c7db3ad6b82",
         "status":"FINISHED",
        "transaction_authorization":{
            "authorization_medium":"authorization_medium_1",
            "captured_value":{
               "amount":560,
               "currency":"BRL"
            },
            "conversion_rate":"1.00",
            "country":"country_3",
            "iof_fee":null,
            "pos_authorization_time":"2019-12-17T18:28:16",
            "value":{
               "amount":560,
               "currency":"BRL"
            }
        },
        "transaction_chargeback":{
            "charged_back_at":"2019-12-17T20:45:31.907317",
            "id":"46ab1de4-8e50-4081-98d5-473660d10189",
            "value":{
               "amount":1,
               "currency":"BRL"
            }
        },
         "type":"outbound_stone_prepaid_card_payment_chargeback"
    }	
}

```

##### Saque com Cartão Stone feito no Banco24Horas

```JSON
{
	"outbound_stone_prepaid_card_withdrawal": {
		"account_id":"ad55491e-c1da-4131-98fb-d74f171a31be",
         "acquirer_code":"acquirer_code",
         "acquirer_name":null,
         "amount":-239,
         "balance_after":3779,
         "balance_before":4018,
         "card_acceptor":{
            "city":"my city_3",
            "country":"country_6",
            "mcc":"mcc_3",
            "name":"card_acceptor_name_3"
         },
         "card_last_four_digits":"5851",
         "created_at":"2019-12-17T19:00:03Z",
         "fee_amount":0,
         "id":"b56471cf-34de-4305-aba4-de9113388077",
         "operation":"debit",
         "operation_amount":239,
         "operation_id":"7d6146f8-dd2d-4c93-832d-77215d8c772e",
         "status":"REFUNDED",
         "transaction_authorization":{
            "authorization_medium":"authorization_medium_3",
            "captured_value":{
               "amount":239,
               "currency":"BRL"
            },
            "conversion_rate":"1.00",
            "country":"country_7",
            "iof_fee":null,
            "pos_authorization_time":"2019-12-17T18:33:14",
            "value":{
               "amount":239,
               "currency":"BRL"
            }
         },
         "type":"outbound_stone_prepaid_card_withdrawal"
	}
}
	
```

##### Devolução de Saque feito no Banco24Horas

```JSON
{
	"outbound_stone_prepaid_card_withdrawal_refund": {            
		 "account_id":"ad55491e-c1da-4111-38fb-d74f171a31be",
         "acquirer_code":"acquirer_code",
         "acquirer_name":null,
         "amount":239,
         "balance_after":4167,
         "balance_before":3928,
         "card_acceptor":{
            "city":"my city_3",
            "country":"country_6",
            "mcc":"mcc_3",
            "name":"card_acceptor_name_3"
         },
         "card_last_four_digits":"5851",
         "created_at":"2019-12-17T19:02:59Z",
         "fee_amount":0,
         "id":"61752b23-96d3-4dab-b0fd-6b8ec2533a11",
         "operation":"credit",
         "operation_amount":239,
         "operation_id":"7d6146f8-dd2d-4c93-822d-73215d8c772e",
         "status":"FINISHED",
         "transaction_authorization":{
            "authorization_medium":"authorization_medium_3",
            "captured_value":{
               "amount":239,
               "currency":"BRL"
            },
            "conversion_rate":"1.00",
            "country":"country_7",
            "iof_fee":null,
            "pos_authorization_time":"2019-12-17T18:33:14",
            "value":{
               "amount":239,
               "currency":"BRL"
            }
         },
         "type":"outbound_stone_prepaid_card_withdrawal_refund"
      }	
}

```

##### Recebimento de salário

```JSON
{
	"salary": {
		"account_id":"ad55391e-c1da-4111-98fb-d74f171a31be",
         "amount":164,
         "balance_after":39215516,
         "balance_before":39215352,
         "counter_party":{
            "account":{
               "account_code":"473603",
               "branch_code":"1",
               "institution":"16501555",
               "institution_name":"Stone Pagamentos S.A."
            },
            "entity":{
               "document":"87939015000106",
               "document_type":"cnpj",
               "name":"Amazing Corporation S.A."
            }
         },
         "created_at":"2019-09-13T22:27:39Z",
         "id":"fff5eb35-63bb-44a9-9640-128c97606710",
         "operation":"credit",
         "status":"FINISHED",
         "type":"salary"
	}
}
	
```

##### Portabilidade de salário

```JSON	
{
	"salary_portability": {            
		"account_id":"ad55431e-c1da-4111-98fb-d74f171a31be" 
        "amount":10000,
        "balance_after":5992000,
        "balance_before":5982000,
        "counter_party": {
            "account":{
               "account_code":"473603",
               "branch_code":"1",
               "institution":"16501555", 
               "institution_name": "ITAÚ UNIBANCO S.A."
			}
        "created_at":"2019-09-13T22:27:39Z",
        "id":"fff5eb35-63bb-44a9-9640-128c97606710",
        "operation": "debit"
        "status": "FINISHED"
        "type": "salary_portability"
      }	
}

```

##### Devolução de salário pela intituição de portabilidade

```JSON
{
	"salary_portability_refund": {
		"account_id":"477f8576-ca83-462b-be73-dc28cc6490c3",
        "amount":200,
        "balance_after":522283672,
        "balance_before":522283472,
        "counter_party":{
            "account":{
               "account_code":"34",
               "branch_code":"0001",
               "institution":"60746948",
               "institution_name":"Banco Bradesco S.A."
            }
        },
        "created_at":"2020-06-26T15:33:14Z",
        "id":"7270d918-df3d-4a62-8de6-11f3a3b36aa7",
        "operation":"credit",
        "refund_reason_code":"4",
        "refund_reason_description":"Mensagem Inválida para o Tipo de Transação ou Finalidade.",
        "status":"FINISHED",
        "type":"salary_portability_refund"
	}
}
```

##### Devolução de salário pela intituição de portabilidade (Em casos de cancelamento)

```JSON
{
	"salary_portability_employer_refund": {            
		 "amount":-200,
         "balance_after":522283472,
         "balance_before":522283672,
         "counter_party":{
            "entity":{
               "document":"99999999999",
               "document_type":"cpf",
               "name":"Nome da Pessoa"
            }
         },
         "created_at":"2020-06-26T15:33:14Z",
         "id":"b9f3722b-9a34-4a89-a94a-9285ba730c50",
         "operation":"debit",
         "status":"FINISHED",
         "type":"salary_portability_employer_refund"
    }	
}

```

