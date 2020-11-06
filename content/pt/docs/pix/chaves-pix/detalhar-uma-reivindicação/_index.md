---
title: "Detalhar reivindicação"
linkTitle: "Detalhar reivindicação"
date: 2020-09-17T18:00:00-03:00
lastmod: 2020-09-17T18:00:00-03:00
weight: 9
draft: false
description: >

---

##### **Request**

```http request
GET /api/v1/pix/:account_id/entry_claims/:claim_id
```

##### **Response**

```http request
200 OK
```
Body
```text
{
  "id": "40346adc-74f3-4c4e-8275-73ba78993491",
  “claim_type”: “portability”,
  "status": "waiting_resolution",
  "origin": "external",
  "origin_ispb": "1234567890",
  “created_at”: "“2020- 09-27T03:00:00Z”,
  “updated_at”: "2020-09-27T06:00:00Z", 
  “expires_at”: "2020-09-30T03:00:00Z",
  "beneficiary_account": {
     "branch_code": “0001”,
     "account_code": "00016583",
     "account_type": "CC",
     "opened_at": "2019-11-18T03:00:00Z"
  },
  "beneficiary_entity": {
     "name": “0001”,
     "document_type": "cpf",
     "document": "13152256685"
  },
  "key_type": "phone",
  "key": "+5510998765432",
  "events": [
   {
      "id": "38963369-533c-42aa-a49e-b5369ff4bd52",
      "created_at": "20200-09-18T03:00:00Z",
      "type": "created",
      "from_status": null,
      "to_status": "active"
    },
    {
      "id": "9bac50e2-c6ad-4193-8263-7170046a85a3",
      "created_at": "20200-09-22T03:00:00Z",
      "type": "portability_requested",
      "from_status": "active",
      "to_status": "portability_pending"
    }
  ]
}
```
