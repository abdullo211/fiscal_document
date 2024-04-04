После отправки оплаты в Payme, Click, Uzum в ответе получаем
1. Номер телефона
2. Payment ID
Это нужно будет отправить вместе с /order в "extra_info" и так же выбрать соответствующий ЭПС
# CLICK PASS / Оплата через CLICK PASS

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
  "payment_id": [payment_id],
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
    "amount": 1,
    "transaction_id": "0e436d79-f100-4373-b12a-1f238b558054",
    "payment_id": "644113a290a5eba4298f05d5",
    "inn": "123456789",
    "qr_code": "50501010793410469483",
    "kkm_id": "00000001",
    "device_id": "00000001",
    "status": "successfully",
    "message": "successfully payment",
    "client_phone_number": "998946532140"
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

# CLICK Fiscalization check / Отправка фискального чека в Click

Operation for send fiscalization check to CLICK

**URL** : `/payment/click_confirm`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
    "payment_id": [Payment_id],
    "qr_code": [URL cheka],    
}
```
**Content** :
```json
{
    "payment_id":"2354512461",
    "qr_code":"https://ofd.soliq.uz/check?t=UZ170703100597&r=2421&c=20230104121801&s=514343190161",    
}
```

## Response
**Success example**
```json
{
    "data": {
        "inn": "000000000",
        "payment_id": "2354512461",
        "qr_code": "https://ofd.soliq.uz/check?t=UZ170703100597&r=2904&c=20230222120100&s=113075569254",
        "status": "successfully",
        "error": null
    },
    "error": null,
    "is_success": true
}
```
**Error example**
```json
{
     "data": null,
    "error": {
        "code": 7,
        "message": "{\"payment_id\":[\"This field may not be blank.\"]}",
        "data": null
    },
    "is_success": false
}
```


# PAYME GO / Оплата через PAYME GO

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
  "payment_id": [payment_id],
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
    "amount": 1,
    "transaction_id": "0e436d79-f100-4373-b12a-1f238b558054",
    "payment_id": "644113a290a5eba4298f05d5",
    "inn": "123456789",
    "qr_code": "50501010793410469483",
    "kkm_id": "00000001",
    "device_id": "00000001",
    "status": "successfully",
    "message": "successfully payment",
    "client_phone_number": "998946532140"
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


# PAYME Fiscalization check / Отправка фискального чека в Payme

Operation for send fiscalization check to PayMe

**URL** : `/payment/payme_confirm`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
    "payment_id": [Payment_id],
    "receipt_id": [Number check],
    "qr_code": [URL cheka],
    "fiscal_sign": [Fiscal priznak cheka]
}
```
**Content** :
```json
{
    "payment_id":"63b5282a6f47f572807fd53e",
    "receipt_id":"2421",
    "qr_code":"https://ofd.soliq.uz/check?t=UZ170703100597&r=2421&c=20230104121801&s=514343190161",
    "fiscal_sign":"514343190161"
}
```

## Response
**Success example**
```json
{
    "data": {
        "id": 123,
        "result": {
            "receipt": {
                "_id": "63b1dc4f49a2bcd2132c39f3",
                "create_time": 1672600657448,
                "pay_time": 1672600657716
            }
        },
        "error": null
    },
    "error": null,
    "is_success": true
}
```
**Error example**
```json
{
    "data": null,
    "error": {
        "code": 7,
        "message": "{\"fiscal_sign\":[\"This field may not be null.\"]}",
        "data": null
    },
    "is_success": false
}
```

# UZUM FASTPAY / Оплата через UZUM FAST PAY

Operation for create paymen via UZUM FASTPAY

**URL** : `/payment/uzum`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price],
  "qr_code": [Qr code from UZUM FAST PAY],
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
  "payment_id": [payment_id],
  "payment_status": [Payment status], 
  "error_code,": [Error code],
  "error_message": [Error message],
  "is_success": [is success response] 
}
```

**Success example**
**Code** : `200 OK`

**Content** :
```{
  "data": {
    "payment_id": "bb75f609-6d97-4b45-9ed3-80e5fcd19ef1",
    "payment_status": "SUCCESS",
    "error_code": "0",
    "error_message": null,
    "client_phone_number": "998946532140"
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

# UZUM Fiscalization check / Отправка фискального чека в Uzum

Operation for send fiscalization check to UZUM

**URL** : `/payment/uzum_confirm`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
    "payment_id": [Payment_id],
    "qr_code": [URL cheka],    
}
```
**Content** :
```json
{
    "payment_id":"7e577908-6851-4a8d-ac1d-bdd17002f96b",
    "qr_code":"https://ofd.soliq.uz/check?t=UZ170703100597&r=2421&c=20230104121801&s=514343190161",    
}
```

## Response
**Success example**
```json
{
  "data": {
    "payment_id": "7e577908-6851-4a8d-ac1d-bdd17002f96b",
    "payment_status": "SUCCESS",
    "error_code": "0",
    "error_message": null,
    "client_phone_number": null
  },
  "error": null,
  "is_success": true
}
```

# Anorbank / Оплата через AnorCheck

Operation for create paymen via AnorCheck

**URL** : `/payment/anor`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price],
  "qr_code": [Qr code from AnorCheck],
}
```
**Content** :
```{
	"amount":500,
	"qr_code":"880101698207133392"
}
```

## Response
**Success example**
```json
{
    "data": {
        "transaction_id": "05a447d7-ad64-4b95-931e-951b624b6534",
        "status": "successfully",
        "message": null,
        "error_code": null,
        "payment_id": 658,
        "error_note": null,
        "payment_status": 2,
        "phone_number": "998946532140",
        "card_number": "860014******3145"
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

# Anor Fiscalization check / Отправка фискального чека в Anor

Operation for send fiscalization check to Anor

**URL** : `/payment/anor_confirm`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
    "transaction_id": [Payment_id],
    "qr_code": [URL cheka],    
}
```
**Content** :
```json
{
"qr_code":"https://ofd.soliq.uz/check?t=UZ170703100597&r=6013&c=20231201160732&s=025561534771",
"transaction_id":"05a447d7-ad64-4b95-931e-951b624b6534"
} 
```

## Response
**Success example**
```json
{
    "data": {
        "message": null,
        "error_code": null,
        "payment_id": null,
        "transaction_id": "05a447d7-ad64-4b95-931e-951b624b6534"
    },
    "error": null,
    "is_success": true
}
```
**Error example**
```json
{
     "data": null,
    "error": {
        "code": 7,
        "message": "{\"payment_id\":[\"This field may not be blank.\"]}",
        "data": null
    },
    "is_success": false
}
```

# Humo / Оплата через терминал (Ingenico iPP 320, Lane 3000, Lane 7000) Humo

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
```json
{
    "data": {
        "message": "           ОБЫЧНЫЙ ТОВАР\n
ID Терминала:09110004  Номер смены 4\
nID Организации:010950461213101 \n
                             Чек\n
340\n
               Оплата\n
              ОДОБРЕНО\n
СУММА(AMOUNT):             10.00 UZS\n
КОМИССИЯ(SURCHARGE):        0.10 UZS\n
ИТОГО(TOTAL):              10.00 UZS\n
AID: A0860001000001  HUMO- Cless EMV\n
TVR: 0000808001\n
Карта: HUMO              Срок: 01/25\n
        986009******7856:01\n
Код авторизации: 635842 \n
                     Код ответа:\n
000\n
RRN:408005356147 \n
              Дата:29/09/23\n
14:07:01\n
Univ. EMV POS 1.0.0/(MP) /675\n
====================================\n",
	"ppt_id": "408005356147"
    },
    "error": null,
    "is_success": true
}
```

# UzCard / Оплата через терминал (PAX A35) UzCard

Operation for create paymen via UzCard PinPad

**URL** : `/payment/uzcard`

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
```json
{
    "data": {
        "message": "PAX A35 Uzcard POS v1.5.0\nMerchant: Technology-7\nAddress: Tashkent, Uzbekistan\n
Date/Time: 2024-04-04 11:22:13\n
MID: 000000009052147\n
TID: 00000166\n
Operation: Оплата\n
Invoice: 474\nCARD: 626291******5674(БЕСКОНТАКТ(W))\n
Card Holder: TCARD/ARCA\n
Total Amount: 50000\n
Currency:  UZS\n
Auth Code: \n
Resp Code: 000\n
RRN: 010965628751\n
PIN: \n
TVR: , TSI: \n",
        "ppt_id": "010965628751"
    },
    "error": null,
    "is_success": true
}
```
