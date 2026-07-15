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
| order_id | integer | Yes | Order ID/ID заказа |
| print | boolean | No | Print QR on receipt/Печатать QR на чеке |
| tip_card | string | No | Card number for tips/Номер карты для чаевых |
| tip_card_expire | string | No | Tip card expiry (MMYY)/Срок действия карты |
| sms_phone_number | string | No | Phone to send payment link/Телефон для ссылки оплаты |
| banners | array | No | Banners to print before the Scan2Pay QR/Баннеры для печати перед QR Scan2Pay |
