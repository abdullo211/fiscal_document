# CLICK PASS

Operation for create paymen via CLICK PASS

**URL** : `/payment/click`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price],
  "qr_code": [Qr code from CLICK PASS],
}
```
**Content** :
```{
	"amount":500,
	"qr_code":"880101698207133392"
}
```

## Response

```json
{
 "data":{
  "status_code": [status code], 
  "status": [Status message],
  "message": [click response message],
  "transaction_id": [transaction_uuid],
  "amount": [Price],
   "qr_code": [Qr code from CLICK PASS],
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

**Success example**
**Code** : `200 OK`

**Content** :
```{
    "data": {
        "status_code": 0,
        "status": "successfully",
        "message": "Успешно подтвержден",
        "transaction_id": "ee000d20-b260-4b17-995a-a7bd113bdb22",
        "qr_code": "880101698207133392"
    },
    "error": null,
    "is_success": true
}
```
**Error example**
**Condition** : If 'Fiscal module not initialized'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 104,
    "message": "BILLING_ERROR",
    "data": null
    },
"is_success": false 
}
```


# PAYME GO

Operation for create paymen via PAYME GO

**URL** : `/payment/payme`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price],
  "qr_code": [Qr code from PAYME GO],
}
```
**Content** :
```{
	"amount":500,
	"qr_code":"880101698207133392"
}
```

## Response

```json
{
 "data":{
  "status": [status code: success,error], 
  "message": [click response message],
  "transaction_id": [transaction_uuid],
  "amount": [Price],
   "qr_code": [Qr code from PAYME GO],
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

**Success example**
**Code** : `200 OK`

**Content** :
```{
    "data": {
        "status_code": 0,
        "status": "successfully",
        "message": "Успешно подтвержден",
        "transaction_id": "ee000d20-b260-4b17-995a-a7bd113bdb22",
        "qr_code": "880101698207133392"
    },
    "error": null,
    "is_success": true
}
```
**Error example**
**Condition** : If 'Fiscal module not initialized'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 104,
    "message": "BILLING_ERROR",
    "data": null
    },
"is_success": false 
}
```
