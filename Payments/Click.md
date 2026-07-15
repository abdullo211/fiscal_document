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
  "client_phone_number": [Client phone number],
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
| data.status_code | integer | Provider status code/Код статуса провайдера |
| data.amount | integer | Payment amount/Сумма оплаты |
| data.transaction_id | string | Transaction UUID/UUID транзакции |
| data.payment_id | string | Payment ID/ID оплаты |
| data.qr_code | string | QR code/QR-код |
| data.status | string | Status/Статус |
| data.message | string | Status message/Сообщение |
| data.client_phone_number | string or null | Client phone/Телефон клиента |

**Success example**
**Code** : `200 OK`

**Content** :
```{
  "data": {
    "status_code": 0,
    "amount": 1,
    "transaction_id": "0e436d79-f100-4373-b12a-1f238b558054",
    "payment_id": "644113a290a5eba4298f05d5",
    "qr_code": "50501010793410469483",
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
