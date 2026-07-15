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
| data.client_phone_number | string or null | Client phone/Телефон клиента |

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
