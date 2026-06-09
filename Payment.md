После отправки оплаты в Payme, Click, Uzum в ответе получаем
1. Номер телефона
2. Payment ID
Это нужно будет отправить вместе с /order в "extra_info" и так же выбрать соответствующий ЭПС

## Common response wrapper

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data | object or null | Response data/Данные ответа |
| error.code | integer | Error code/Код ошибки |
| error.message | string | Error message/Сообщение об ошибке |
| error.data | string or null | Extra error data/Дополнительные данные |
| is_success | boolean | Success flag/Признак успешного ответа |

## Common payment request (Click, Payme, Uzum, Anor)

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| amount | integer | Yes | Payment amount in tiyin (×100)/Сумма оплаты в тийинах |
| qr_code | string | Yes | QR code from payment app/QR-код из приложения оплаты |

## Common confirm request (Click, Payme, Uzum)

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| payment_id | string | Yes | Payment ID from provider/ID оплаты от провайдера |
| qr_code | string | Yes | Fiscal receipt URL/URL фискального чека |

## Pinpad return request (Humo, UzCard)

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| amount | integer | Yes | Amount in tiyin (×100)/Сумма в тийинах |
| request_id | string or integer | Yes | RRN from bank slip/RRN с банковского слипа |
| is_return | boolean | Yes | Return flag/Признак возврата |

## Scan2pay request

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| amount | integer | Yes | Payment amount in tiyin (×100)/Сумма в тийинах |
| order_id | string | Yes | Order ID/ID заказа |
| print | boolean | No | Print QR on receipt/Печатать QR на чеке |
| tip_card | string | No | Card number for tips/Номер карты для чаевых |
| tip_card_expire | string | No | Tip card expiry (MMYY)/Срок действия карты |
| sms_phone_number | string | No | Phone to send payment link/Телефон для ссылки оплаты |

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

See [Common payment request](#common-payment-request-click-payme-uzum-anor) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.amount | integer | Payment amount/Сумма оплаты |
| data.transaction_id | string | Transaction UUID/UUID транзакции |
| data.payment_id | string | Payment ID/ID оплаты |
| data.inn | string | Company TIN/ИНН |
| data.qr_code | string | QR code/QR-код |
| data.kkm_id | string | KKM ID/ID ККМ |
| data.device_id | string | Device ID/ID устройства |
| data.status | string | Status/Статус |
| data.message | string | Status message/Сообщение |
| data.client_phone_number | string | Client phone/Телефон клиента |

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

See [Common confirm request](#common-confirm-request-click-payme-uzum) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.inn | string | Company TIN/ИНН |
| data.payment_id | string | Payment ID/ID оплаты |
| data.qr_code | string | Fiscal receipt URL/URL фискального чека |
| data.status | string | Status/Статус |
| data.error | null | Always null on success/Всегда null при успехе |

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

See [Common payment request](#common-payment-request-click-payme-uzum-anor) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.amount | integer | Payment amount/Сумма оплаты |
| data.transaction_id | string | Transaction UUID/UUID транзакции |
| data.payment_id | string | Payment ID/ID оплаты |
| data.inn | string | Company TIN/ИНН |
| data.qr_code | string | QR code/QR-код |
| data.kkm_id | string | KKM ID/ID ККМ |
| data.device_id | string | Device ID/ID устройства |
| data.status | string | Status/Статус |
| data.message | string | Status message/Сообщение |
| data.client_phone_number | string | Client phone/Телефон клиента |

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
    "qr_code": [URL cheka],
}
```
**Content** :
```json
{
    "payment_id":"63b5282a6f47f572807fd53e",
    "qr_code":"https://ofd.soliq.uz/check?t=UZ170703100597&r=2421&c=20230104121801&s=514343190161",
}
```

See [Common confirm request](#common-confirm-request-click-payme-uzum) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.id | integer | Response ID/ID ответа |
| data.result.receipt._id | string | Payme receipt ID/ID чека Payme |
| data.result.receipt.create_time | integer | Receipt create timestamp/Время создания |
| data.result.receipt.pay_time | integer | Payment timestamp/Время оплаты |
| data.error | null | Always null on success/Всегда null при успехе |

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
  "error_code": [Error code],
  "error_message": [Error message],
  "is_success": [is success response] 
}
```

See [Common payment request](#common-payment-request-click-payme-uzum-anor) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.payment_id | string | Payment UUID/UUID оплаты |
| data.payment_status | string | Status (`SUCCESS`, etc.)/Статус оплаты |
| data.error_code | string | Error code (`0` = success)/Код ошибки |
| data.error_message | string or null | Error message/Сообщение об ошибке |
| data.client_phone_number | string | Client phone/Телефон клиента |

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

See [Common confirm request](#common-confirm-request-click-payme-uzum) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.payment_id | string | Payment UUID/UUID оплаты |
| data.payment_status | string | Status/Статус |
| data.error_code | string | Error code/Код ошибки |
| data.error_message | string or null | Error message/Сообщение об ошибке |
| data.client_phone_number | string or null | Client phone/Телефон клиента |

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

See [Common payment request](#common-payment-request-click-payme-uzum-anor) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.transaction_id | string | Transaction UUID/UUID транзакции |
| data.status | string | Status/Статус |
| data.message | string or null | Message/Сообщение |
| data.error_code | string or null | Error code/Код ошибки |
| data.payment_id | integer | Payment ID/ID оплаты |
| data.error_note | string or null | Error note/Примечание об ошибке |
| data.payment_status | integer | Payment status code/Код статуса оплаты |
| data.phone_number | string | Client phone/Телефон клиента |
| data.card_number | string | Masked card number/Маскированный номер карты |

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

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| transaction_id | string | Yes | Transaction ID from Anor payment/ID транзакции из оплаты Anor |
| qr_code | string | Yes | Fiscal receipt URL/URL фискального чека |

## Response

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string or null | Message/Сообщение |
| data.error_code | string or null | Error code/Код ошибки |
| data.payment_id | string or null | Payment ID/ID оплаты |
| data.transaction_id | string | Transaction ID/ID транзакции |

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
  "amount": 1000
}
```

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| amount | integer | Yes | Amount in tiyin (×100)/Сумма в тийинах |

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Bank slip text/Текст банковского слипа |
| data.ppt_id | string | RRN reference/RRN операции |

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

# Humo / Универсальная отмена (в рамках 1 смены) через пинпад (Ingenico iPP 320, Lane 3000, Lane 7000) Humo

Operation for create paymen via Humo PinPad

**URL** : `/payment/xumo`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "request_id": [Request ID / RRN с банковского слипа],
  "amount": [Payment price],
  "is_return": [true]
}
```
**Content** :
```json
{
  "request_id": 408005356147,
  "amount": 1000,
  "is_return": true
}
```

See [Pinpad return request](#pinpad-return-request-humo-uzcard) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Bank slip text/Текст банковского слипа |
| data.ppt_id | string | RRN reference/RRN операции |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
    "data": {
        "message": "
            ОБЫЧНЫЙ ТОВАР
         IP OOO JETI ASPAN
      TOSHKENT, BUNYODKOR 9 UY
ID Терм.:34112204      Номер смены 1
ID Орг.:011760574070401       Чек 14
          Отмена (CANCEL)
              ОДОБРЕНО
         ОПЕРАЦИЯ ОТМЕНЕНА
СУММА:                    10.00 UZS
AID:A0860001000001   HUMO- Cless EMV
Карта:HUMO
        986018******9831:01
Код авториз.:731333   Код ответа:400
RRN(ссылка) :416311639412
Дата:11/06/24 17:39:54
Univ. EMV POS 1.0.0/(MP) /681
                ***
@humocardbot-информация по вашей
карте
====================================

	"ppt_id": "416311639412"
    },
    "error": null,
    "is_success": true
}
```

# Humo / Сверка итогов терминал (Ingenico iPP 320, Lane 3000, Lane 7000) Humo

Operation for reconciliation of results via Humo PinPad

**URL** : `/payment/xumo_close`

**Method** : `GET`

**Auth required** : NO

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Reconciliation report text/Текст отчёта сверки |
| data.ppt_id | string or null | RRN reference/RRN операции |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
    "data": {
        "message": "====================================\n        Отчет закрытия смены\n           Итоги совпали\nДата:08/07/24         Время:11:45:22\n             Тест humo\n           Краткий отчет\nТерминал:                   09110004\nДата:08/07/24         Время:11:45:23\n------------------------------------\n                 -\n           Отчет окончен\n====================================\n====================================\n        Отчет закрытия смены\n====================================\n           Сверка итогов\nДата:08/07/24         Время:11:45:26\n====================================\nТерминал ID: 00000031\nID магазина:  000000009002143\n           -0000000000.00\n           Итоги совпали\nДата:08/07/24         Время:11:45:27\n             Тест humo\n           Краткий отчет\nТерминал:                   00000031\nДата:08/07/24         Время:11:45:27\n------------------------------------\n                 -\n           Отчет окончен\n====================================\n",
        "ppt_id": null
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
  "amount": 50000
}
```

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| amount | integer | Yes | Amount in tiyin (×100)/Сумма в тийинах |

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Bank slip text/Текст банковского слипа |
| data.ppt_id | string | RRN reference/RRN операции |

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

# UzCard / Возврат через пинпад PAX A35 UzCard

Operation for create paymen via PAX A35 UzCard

**URL** : `/payment/uzcard`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "request_id": [Request RRN / Номер RRN с банковского слипа],
  "amount": [Payment price],
  "is_return": [true]
}
```
**Content** :
```json
{
  "request_id": "010965270742",
  "amount": 30000,
  "is_return": true
}
```

See [Pinpad return request](#pinpad-return-request-humo-uzcard) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Bank slip text/Текст банковского слипа |
| data.ppt_id | string | RRN reference/RRN операции |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
    "data": {
        "message": "
            OOO TEST TIME
        Tashkent, Main str
       БЕСКОНТАКТНАЯ ОПЕРАЦИЯ
Номер операции:                  168
Терминал:                   00000013
Торговец:            000000900227899
Версия ПО:        SKappay v1.7.0_rc2
SN:                       2290268839
RRN                     010968002727
Дата             2025-03-07 14:54:27
Карта               544081******5040
Тип:               UZCARD-MASTERCARD
 
 
              Возврат
             500.00 UZS
              Одобрено
          Код ответа:000 
, pptId=010968002727), error=null, isSuccess=true
}
```

# UZCARD / Сверка итогов терминал (PAX A35) UZCARD

Operation for reconciliation of results via Uzcard PinPad

**URL** : `/payment/uzcard_close`

**Method** : `GET`

**Auth required** : NO

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Reconciliation report text/Текст отчёта сверки |
| data.ppt_id | string or null | RRN reference/RRN операции |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
    "data": {
        "message": "====================================\n        Отчет закрытия смены\n           Итоги совпали\nДата:08/07/24         Время:11:45:22\n             Тест humo\n           Краткий отчет\nТерминал:                   09110004\nДата:08/07/24         Время:11:45:23\n------------------------------------\n                 -\n           Отчет окончен\n====================================\n====================================\n        Отчет закрытия смены\n====================================\n           Сверка итогов\nДата:08/07/24         Время:11:45:26\n====================================\nТерминал ID: 00000031\nID магазина:  000000009002143\n           -0000000000.00\n           Итоги совпали\nДата:08/07/24         Время:11:45:27\n             Тест humo\n           Краткий отчет\nТерминал:                   00000031\nДата:08/07/24         Время:11:45:27\n------------------------------------\n                 -\n           Отчет окончен\n====================================\n",
        "ppt_id": null
    },
    "error": null,
    "is_success": true
}
```

# UzQR / Оплата через UzQR (one_qr)

Оплата через динамический QR-код UzQR. POS генерирует QR, покупатель сканирует его из банковского приложения.

Интеграция состоит из двух шагов:
1. Создать инвойс — получить `invoice_id` и `qr_text` для отображения QR покупателю
2. Запросить статус оплаты — fbox держит соединение открытым и сам делает polling каждые 3 секунды (до 2 минут), ответ возвращается только при финальном статусе

---

## Common response wrapper

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data | object or null | Response data/Данные ответа |
| error.code | integer | Error code/Код ошибки |
| error.message | string | Error message/Сообщение об ошибке |
| is_success | boolean | Success flag/Признак успешного ответа |

## Payment status values / Статусы оплаты

| Value | Description EN/RU |
| ----- | ----------------- |
| 1 | In progress / В процессе |
| 2 | Success / Успешно |
| 3 | Declined / Отклонено |

---

# UzQR / Оплата через UzQR (one_qr)

Оплата через динамический QR-код UzQR. POS генерирует QR, покупатель сканирует его из банковского приложения.

Интеграция состоит из двух шагов:
1. Создать инвойс — получить `invoice_id` и `qr_text` для отображения QR покупателю
2. Запросить статус оплаты — fbox держит соединение открытым и сам делает polling каждые 3 секунды (до 2 минут), ответ возвращается только при финальном статусе

---

## Common response wrapper

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data | object or null | Response data/Данные ответа |
| error.code | integer | Error code/Код ошибки |
| error.message | string | Error message/Сообщение об ошибке |
| is_success | boolean | Success flag/Признак успешного ответа |

## Payment status values / Статусы оплаты

| Value | Description EN/RU |
| ----- | ----------------- |
| 1 | In progress / В процессе |
| 2 | Success / Успешно |
| 3 | Declined / Отклонено |

---

# UzQR Create Invoice / Создание динамического QR

**URL** : `/payment/one_qr/create`

**Method** : `POST`

**Auth required** : NO

## Request

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| external_id | string | Yes | Unique operation ID on POS side, max 20 chars / Уникальный ID операции на стороне POS, до 20 знаков |
| amount | string | Yes | Amount in UZS with dot separator, e.g. `"100.01"` / Сумма в сумах с разделителем точка |
| print | boolean | No | If `true` — print banners and QR code on the receipt printer. If `false` or omitted — only return data / Если `true` — печатать баннеры и QR-код на принтере. Если `false` или не передан — только вернуть данные |
| banners | array | No | Optional banners to print before the QR code (same format as `/print/banner`). Used only when `print=true` / Баннеры для печати перед QR-кодом (тот же формат, что и `/print/banner`). Используются только при `print=true` |

> `fiscal_module` is set automatically from device config — do not send it / устанавливается автоматически из конфига устройства

**Minimal request:**

```json
{
  "external_id": "EXT001",
  "amount": "100.00"
}
```

**Request with printing:**

```json
{
  "external_id": "EXT001",
  "amount": "100.00",
  "print": true,
  "banners": [
    {
      "type": "text",
      "data": "Thank you for your purchase!",
      "style": { "align": "center", "is_bold": true }
    }
  ]
}
```

## Response

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.invoice_id | string | UzQR invoice ID, use for status polling / ID инвойса, использовать для запроса статуса |
| data.qr_text | string | QR content to display / Текст QR для отображения |

**Success example**

**Code** : `200 OK`

```json
{
  "data": {
    "invoice_id": "INVC134B7FEFED34BC3B470B8",
    "qr_text": "00020101021240350012qr-online.uz0109987650001..."
  },
  "error": null,
  "is_success": true
}
```

**Error example**

**Condition** : UzQR endpoint or API key not configured in device config

**Code** : `200 OK`

```json
{
  "data": null,
  "error": {
    "code": 104,
    "message": "UzQR endpoint not configured",
    "data": null
  },
  "is_success": false
}
```

**Error example**

**Condition** : UzQR authorization failed (wrong INN or API key)

**Code** : `200 OK`

```json
{
  "data": null,
  "error": {
    "code": 1001,
    "message": "Ошибка авторизации UzQR. Проверьте настройки подключения.",
    "data": null
  },
  "is_success": false
}
```

---

# UzQR Payment Status / Статус оплаты UzQR

**URL** : `/payment/one_qr/status?invoice_id={invoice_id}`

**Method** : `GET`

**Auth required** : NO

> **Important / Важно**: This endpoint uses **long polling** — fbox internally polls UzQR every 3 seconds (up to 2 minutes) and responds only when a final status is received. Set client timeout to at least **150 seconds**.
>
> **Важно**: Этот endpoint использует **long polling** — fbox внутри опрашивает UzQR каждые 3 секунды (до 2 минут) и отвечает только при финальном статусе. Установите таймаут клиента не менее **150 секунд**.

## Request

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| invoice_id | string | Yes | Invoice ID from create response / ID инвойса из ответа создания |

```
GET /payment/one_qr/status?invoice_id=INVC134B7FEFED34BC3B470B8
```

## Response

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.invoice_id | string | Invoice ID / ID инвойса |
| data.status | integer | Payment status: 1=in progress, 2=success, 3=declined / Статус оплаты |
| data.pay_id | string or null | Payment ID, present when status=2 / ID платежа, есть при статусе 2 |
| data.payer_phone | string or null | Payer phone, e.g. `+998901234567` / Телефон плательщика |
| data.card_type | string or null | Card type: 1=corporate, 2=personal, 3=social / Тип карты |
| data.card_no | string or null | Masked card number, e.g. `8600********1234` / Маскированный номер карты |
| data.fiscal_module | string | Fiscal module number / Номер фискального модуля |

**Success example — payment completed**

**Code** : `200 OK`

```json
{
  "data": {
    "invoice_id": "INVC134B7FEFED34BC3B470B8",
    "status": 2,
    "pay_id": "PAY12345678901234567",
    "payer_phone": "+998901234567",
    "card_type": "2",
    "card_no": "8600********1234",
    "fiscal_module": "12345678901234"
  },
  "error": null,
  "is_success": true
}
```

**Success example — payment in progress (still polling)**

**Code** : `200 OK`

```json
{
  "data": {
    "invoice_id": "INVC134B7FEFED34BC3B470B8",
    "status": 1,
    "pay_id": null,
    "payer_phone": null,
    "card_type": null,
    "card_no": null,
    "fiscal_module": "12345678901234"
  },
  "error": null,
  "is_success": true
}
```

> fbox will continue polling internally — this response is only returned after timeout (2 min)

**Success example — payment declined**

**Code** : `200 OK`

```json
{
  "data": {
    "invoice_id": "INVC134B7FEFED34BC3B470B8",
    "status": 3,
    "pay_id": null,
    "payer_phone": null,
    "card_type": null,
    "card_no": null,
    "fiscal_module": "12345678901234"
  },
  "error": null,
  "is_success": false
}
```

**Error example**

**Condition** : Invoice not found (polling stops immediately) / Инвойс не найден

**Code** : `200 OK`

```json
{
  "data": null,
  "error": {
    "code": 3001,
    "message": "Операция не найдена.",
    "data": null
  },
  "is_success": false
}
```

---

## UzQR Error Codes / Коды ошибок UzQR

| error_code | Description EN/RU |
| ---------- | ----------------- |
| 1001 | Auth failed — wrong INN or API key / Ошибка авторизации — неверный ИНН или API-ключ |
| 1002 | Access blocked / Доступ заблокирован |
| 2001 | Invalid request params / Некорректные параметры запроса |
| 2002 | Invalid amount format / Некорректный формат суммы |
| 2003 | Invalid external_id format / Некорректный формат external_id |
| 2004 | Invalid fiscal_module / Некорректный номер фискального модуля |
| 3001 | Invoice not found — polling stops / Инвойс не найден — polling прекращается |
| 3002 | Invoice already paid / Инвойс уже оплачен |
| 6001 | Rate limit exceeded — retry later / Превышен лимит запросов |
| 9001 | UzQR internal error — retry later / Внутренняя ошибка UzQR |

---

# Scan2pay / Оплата через сервис Scan2pay

Payment via Scan2pay service

**URL** : `/payment/qr_pay`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price multiplied by 100],
  "order_id": [ORDER ID],
  "print": [false if you don't need to print QR],
  *"tip_card": [Card number for tips or null / Номер карты для чаевых или ноль],
  *"tip_card_expire": [date expire card for tips or null / дата истечения срока действия карты для чаевых или null]
  *"sms_phone_number": [send scan2pay url for payment via sms 998********* or null  /  отправить ссылку scan2pay для оплаты через смс 998********* или null]
}
```
**Content** :
```json
{
  "amount": 500,
  "order_id": "77777",
  "print": false,
  "tip_card": "8600112991130444",
  "tip_card_expire": "0726",
  "sms_phone_number": "998998895989"
}
```

See [Scan2pay request](#scan2pay-request) for request fields.

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.status | string | Status/Статус |
| data.message | string | Payment URL or message/URL оплаты или сообщение |

## Response

```json
{
    "data": {
        "status": "successfully",
        "message": "http://scan2pay.uz/7c545c1e-9a57-4a2f-80dc-b7686023ec04"
    },
    "error": null,
    "is_success": true
}
```

# Status payment Scan2pay / Статус оплаты Scan2pay

Status payment via Scan2pay service

**URL** : `/payment/qr_pay/status`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "order_id": [ORDER ID]
}
```
**Content** :
```json
{
	"order_id":"77777"
}
```

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| order_id | string | Yes | Order ID from `/payment/qr_pay`/ID заказа |

## Response payment has been completed

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.status | string | Response status/Статус ответа |
| data.data.uuid | string | Transaction UUID/UUID транзакции |
| data.data.order_id | string | Order ID/ID заказа |
| data.data.device | string | Device ID/ID устройства |
| data.data.status | string | Payment status/Статус оплаты |
| data.message | string or null | Message/Сообщение |

```json
{
    "data": {
        "status": "successfully",
        "data": {
            "uuid": "1c9389de-c41c-4148-8b46-5d666caffd89",
            "order_id": "77777",
            "device": "00000001",
            "status": "success"
        },
        "message": null
    },
    "error": null,
    "is_success": true
}
```

**Error example There has been no payment yet**
```json
{
    "data": null,
    "error": {
        "code": 105,
        "message": "{\"status\":\"error\",\"message\":\"Transaction not found\"}HTTP Exception 404 Not Found",
        "data": null
    },
    "is_success": false
}
```
