# Authorization

Look through the following examples on how authorizations can be queried either on a detail level or on a summary  level to suit your integration, reporting, reconciliation & product needs.

---

### Example1
<!-- theme: success -->
>**POST** `/v1/authorization/search`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### List all authorizations for a given Day

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/search' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210217",
  "toDate": "20210217",
  "limit": 2
}'
```


<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
   {
      "sourceKey":"1",
      "approvalCode":"Approved",
      "cshbAmount":0,
      "CVVResultKey":"0",
      "lcldt":"02/17/2021 11:15:00 AM",
      "merchandiseCodeKey":"0",
      "timeTaken":1234,
      "fuelPurchaseLocation":null,
      "pumpRegisterNumber":"0",
      "sendModeKey":"1",
      "fuelPurchaseLocationKey":"5814"
   },
   {
      "sourceKey":"0",
      "approvalCode":"Approved",
      "cshbAmount":0.0,
      "CVVResultKey":"0",
      "lcldt":"02/17/2021 08:17:00 AM",
      "merchandiseCodeKey":"0",
      "timeTaken":213,
      "fuelPurchaseLocation":null,
      "pumpRegisterNumber":"5",
      "sendModeKey":"1",
      "fuelPurchaseLocationKey":"5814"
   }
]
```
---

### Example2
<!-- theme: success -->
>**POST** `/v1/authorization/search`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### Fetch selected authorization fields for a given day

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/search' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210217",
  "toDate": "20210217",
  "limit": 3,
  "fields": [
    "AccountNumber","Amount","Currency","PaymentMethod","Network"
  ]
}'
```


<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
   {
      "paymentMethod":"EMV",
      "amount":7.92,
      "currency":"USD",
      "accountNumber":"XXXXXXXXXXXX0000",
      "network":"Master"
   },
   {
      "paymentMethod":"ContactlessChip",
      "amount":14.97,
      "currency":"USD",
      "accountNumber":"XXXXXXXXXXXX1111",
      "network":"Visa"
   },
   {
      "paymentMethod":"CredentialOnFile",
      "amount":15.0,
      "currency":"USD",
      "accountNumber":"XXXXXXXXXXXX2726",
      "network":"Visa"
   }
]
```
---

### Example3
<!-- theme: success -->
>**POST** `/v1/authorization/search`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### search authorizations for an AuthCode, first6 and last4:

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/search' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210217",
  "toDate": "20210217",
  "limit": 1,
  "fields": [
    "AccountNumber","Amount","Currency","PaymentMethod","Network","AuthCode","First6","Last4"
  ],
"authCode": "654321",
  "first6": "123456",
  "last4": "7890"
}'
```

<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
  {
    "last4": "7890",
    "amount": 8.81,
    "authCode": "654321",
    "paymentMethod": "MagneticStripe",
    "currency": "USD",
    "accountNumber": "XXXXXXXXXXXX0000",
    "first6": "123456",
    "network": "Master"
  }
]
```
---

### Example4
<!-- theme: success -->
>**POST** `/v1/authorization/search`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### Fetch all declined transactions for a given day

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/search' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210217",
  "toDate": "20210217",
  "limit": 3,
  "fields": [
    "DeclineReason","AccountNumber","Amount","Currency","PaymentMethod","Network"
  ]
}'
```

<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
   {
      "paymentMethod":"EMV",
      "amount":5.07,
      "currency":"USD",
      "accountNumber":"XXXXXXXXXXXX1111",
      "declineReason":"Approved",
      "network":"Visa"
   },
   {
      "paymentMethod":"EMV",
      "amount":9.27,
      "currency":"USD",
      "accountNumber":"XXXXXXXXXXXX0000",
      "declineReason":"AccountLocked",
      "network":"Visa"
   },
   {
      "paymentMethod":"CredentialOnFile",
      "amount":15.0,
      "currency":"USD",
      "accountNumber":"XXXXXXXXXXXX2222",
      "declineReason":"SuspectedFraud",
      "network":"Discover"
   }
]
```

### Example5
<!-- theme: success -->
>**POST** `/v1/authorization/search`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### Fetch all Authorized transactions for a given store

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/search' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "fromDate": "20210217",
    "toDate": "20210217",
    "limit": 5,
    "fields": [
        "AccountNumber",
        "Amount",
        "Currency",
        "PaymentMethod",
        "Network",
        "SiteID"
    ],
    "siteIDs": [
        325574
    ]
}'

```

<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
  {
    "paymentMethod": "EMV",
    "siteID": 325574,
    "amount": 7.17,
    "currency": "USD",
    "accountNumber": "XXXXXXXXXXXX4444",
    "network": "Master"
  },
  {
    "paymentMethod": "EMV",
    "siteID": 325574,
    "amount": 22.06,
    "currency": "USD",
    "accountNumber": "XXXXXXXXXXXX3333",
    "network": "Master"
  },
  {
    "paymentMethod": "EMV",
    "siteID": 325574,
    "amount": 8.3,
    "currency": "USD",
    "accountNumber": "XXXXXXXXXXXX2222",
    "network": "Amex"
  },
  {
    "paymentMethod": "ContactlessChip",
    "siteID": 325574,
    "amount": 7.42,
    "currency": "USD",
    "accountNumber": "XXXXXXXXXXXX1111",
    "network": "Visa"
  },
  {
    "paymentMethod": "EMV",
    "siteID": 325574,
    "amount": 4,
    "currency": "USD",
    "accountNumber": "XXXXXXXXXXXX0000",
    "network": "Visa"
  }
]
```

### Example6
<!-- theme: success -->
>**POST** `/v1/authorization/summary`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### Fetch the summary of authorizations broken down by the Network for a month

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/summary' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210201",
  "toDate": "20210228",
  "summaryBy": "Network"
}'
```

<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
  {
    "currency": "USD",
    "value": "American Express",
    "countTotal": 1767687,
    "amountTotal": 18075471.93,
    "approvedCount": 1747261
  },
  {
    "currency": "USD",
    "value": "Visa",
    "countTotal": 43385622,
    "amountTotal": 360162124.59999996,
    "approvedCount": 42607416
  },
  {
    "currency": "USD",
    "value": "Mastercard",
    "countTotal": 16225109,
    "amountTotal": 135021987.46,
    "approvedCount": 15885079
  },
  {
    "currency": "USD",
    "value": "Discover",
    "countTotal": 1334641,
    "amountTotal": 11946665.680000002,
    "approvedCount": 1301266
  }
]
```
### Example7
<!-- theme: success -->
>**POST** `/v1/authorization/summary`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### Fetch the summary of authorizations broken down by the Payment Method for a single store for a month.

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/summary' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210201",
  "toDate": "20210228",
  "summaryBy": "PaymentMethod",
  "siteIDs": [
    "325574"
  ]
}'
```


<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
 
  {
    "currency": "USD",
    "value": "Magnetic Stripe",
    "countTotal": 154,
    "amountTotal": 1143.3999999999999,
    "approvedCount": 149
  },
  {
    "currency": "USD",
    "value": "EMV",
    "countTotal": 6636,
    "amountTotal": 55919.21,
    "approvedCount": 6588
  },
  {
    "currency": "USD",
    "value": "Contactless Chip",
    "countTotal": 201,
    "amountTotal": 1610.5700000000002,
    "approvedCount": 199
  },
  {
    "currency": "USD",
    "value": "Mobile & ECommerce",
    "countTotal": 352,
    "amountTotal": 3208.86,
    "approvedCount": 320
  },
  {
    "currency": "USD",
    "value": "Fallback to Mag Stripe",
    "countTotal": 73,
    "amountTotal": 581.89,
    "approvedCount": 73
  },
  {
    "currency": "USD",
    "value": "Credential on File",
    "countTotal": 246,
    "amountTotal": 2013.25,
    "approvedCount": 229
  }
]
```
---

### Example8
<!-- theme: success -->
>**POST** `/v1/authorization/summary`

---

#### Payload Example

<!--
type: tab
title: Request
-->

##### Fetch the summary of authorizations broken down by date for a single store.

```json
curl -X 'POST' \
  'http://localhost:5005/v1/authorization/summary' \
  -H 'accept: application/json' \
  -H 'apiKey: YOUR KEY' \
  -H 'Content-Type: application/json' \
  -d '{
  "fromDate": "20210201",
  "toDate": "20210205",
  "summaryBy": "TxnDay",
  "siteIDs": [
    "325574"
  ]
}'
```


<!--
type: tab
title: Response
-->

##### Successful response (200)

```json
[
  {
    "currency": "USD",
    "value": "20210202",
    "countTotal": 284,
    "amountTotal": 2172.8100000000004,
    "approvedCount": 282
  },
  {
    "currency": "USD",
    "value": "20210201",
    "countTotal": 249,
    "amountTotal": 1860.68,
    "approvedCount": 249
  },
  {
    "currency": "USD",
    "value": "20210204",
    "countTotal": 284,
    "amountTotal": 2254.33,
    "approvedCount": 283
  },
  {
    "currency": "USD",
    "value": "20210203",
    "countTotal": 281,
    "amountTotal": 2029.26,
    "approvedCount": 280
  },
  {
    "currency": "USD",
    "value": "20210205",
    "countTotal": 301,
    "amountTotal": 2506.97,
    "approvedCount": 293
  }
]
```
---