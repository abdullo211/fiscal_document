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
  *"sms_phone_number": [send scan2pay url for payment via sms 998********* or null  /  отправить ссылку scan2pay для оплаты через смс 998********* или null],
  *"banners": [banner objects]
}
```
**Content** :
```json
{
  "amount": 500,
  "order_id": 77777,
  "print": false,
  "tip_card": "8600112991130444",
  "tip_card_expire": "0726",
  "sms_phone_number": "998998895989",
  "banners": []
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
