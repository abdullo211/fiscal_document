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

# Humo

Operation for create paymen via Humo PinPad

**URL** : `/payment/xumo`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price]
}
```
**Content** :
```json
{
  "amount": 50000 (цена в сотых 00)
}
```

**Success example**
**Code** : `200 OK`

**Content** :
```{
	isSuccess=true, 
	message=ОБЫЧНЫЙ ТОВАР
ID Терминала:01000002  Номер смены 1
ID Организации:190339999999902 
                               Чек 6
               Оплата
              ОДОБРЕНО
СУММА:                    500.00 UZS
AID: A0860001000001    HUMO- EMV ICC
TVR: 0000008000TSI:E800
Карта: HUMO              Срок: 01/25
        986009******7856:01
          HUMO CARDTEST14
Введен                   offline-PIN
Код авторизации: 728892 
                     Код ответа:
000
RRN:231511584547 
              Дата:11/11/22
17:01:07
Univ. EMV POS 1.0.0/(MP) /687
 
====================================
```
