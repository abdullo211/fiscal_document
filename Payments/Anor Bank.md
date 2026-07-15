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
| data.error_code | integer or null | Error code/Код ошибки |
| data.payment_id | integer | Payment ID/ID оплаты |
| data.error_note | string or null | Error note/Примечание об ошибке |
| data.payment_status | integer | Payment status code/Код статуса оплаты |
| data.phone_number | string or null | Client phone/Телефон клиента |
| data.card_number | string or null | Masked card number/Маскированный номер карты |

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
| data.error_code | integer or null | Error code/Код ошибки |
| data.payment_id | integer or null | Payment ID/ID оплаты |
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
