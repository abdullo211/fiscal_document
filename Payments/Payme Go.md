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
| data.client_phone_number | string or null | Client phone/Телефон клиента |

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
