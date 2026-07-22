
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

## Send UzQR fiscal receipt / Отправка фискального чека в UzQR

**URL** : `/payment/one_qr/receipt`

**Method** : `POST`

**Auth required** : NO

## Request

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| pay_id | string | Yes | PAY ID from STATUS PAYMENT / Плтаженый ID операции от статуса платежа  |
| fiscal_receipt_url | string | Yes | URL fiscal check from /order/create / URL фискального чека из /order/create |

**Request:**

```json
{
  "pay_id": "PAY12345678901234567",
  "fiscal_receipt_url": "https://example.com/fiscal-receipt/123](https://ofd.soliq.uz/check?t=LG420230601161&r=92927&c=20260617102213&s=117733149112"
}
```

## Response

**Success example**

**Code** : `200 OK`

```json
{
  "data": {},
  "error": null,
  "is_success": true
}
```

**Error example**

**Condition** : UzQR payment transaction not found

**Code** : `200 OK`

```json
{
    "data": null,
    "error": {
        "code": 4001,
        "message": "Платеж не найден.",
        "data": null
    },
    "is_success": false
}
```

**Error example**

**Condition** : D'ont send fiscal url

**Code** : `200 OK`

```json
{
    "data": null,
    "error": {
        "code": 105,
        "message": "fiscal_receipt_url is required",
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

# UzQR Cancel Payment / Отмена оплаты UzQR

**URL** : `/payment/one_qr/cancel`

**Method** : `POST`

**Auth required** : NO

## Request

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| invoice_id | string | Yes | Invoice ID from create response / ID инвойса из ответа создания |

**Request:** 

```json
{
  "invoice_id": "INV8D1EBF7CDCBA44E7BF90D3"
}
```

## Response

**Success example**

**Code** : `200 OK`

```json
{
    "data": {},
    "error": null,
    "is_success": true
}
```

**Error example**

**Condition** : UzQR payment is not found

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

# UzQR Refund Payment / Возврат оплаты UzQR

**Правила**

●	Возврат доступен только для успешной операции.

●	Доступен частичный возврат.

●	POS должен передать сумму возврата в параметре amount.

●	Для полного возврата POS передает полную сумму операции.

●	Для частичного возврата POS передает сумму частичного возврата.

●	Сумма возврата не может быть больше суммы операции.

●	Возврат возможен только по операции, проведенной через этот POS.

●	Причина возврата в POS не требуется.

●	Возврат является асинхронным процессом.

●	UzQR возвращает refund_id.

●	POS использует refund_id для проверки статуса.

●	При попытке отменить уже отмененный платеж UzQR возвращает ошибку.

●	При попытке отменить платеж, недоступный к отмене, UzQR возвращает ошибку.


**URL** : `/payment/one_qr/refund`

**Method** : `POST`

**Auth required** : NO

## Request

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| pay_id | string | Yes | PAY ID from PAYMENT STATUS response / ID платежа из ответа статуса оплаты |
| amount | string | Yes | Amount / Сумма |

**Request:** 

```json
{
  "pay_id": "PAY123456",
  "amount": "1"
}
```

## Response

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.refund_id | string | Refund ID / ID возврата |
| data.status | integer | Status: 1=success |


**Success example**

**Code** : `200 OK`

```json
{
    "data": {
        "refund_id": "REFF5149C4B458F4D7FB",
        "status": 1
    },
    "error": null,
    "is_success": true
}
```

**Error example**

**Condition** : UzQR payment is not found

**Code** : `200 OK`

```json
{
    "data": null,
    "error": {
        "code": 4001,
        "message": "Платеж не найден.",
        "data": null
    },
    "is_success": false
}
```

# UzQR Refund Status / Статус Возврата UzQR

**URL** : `/payment/one_qr/refund/status?refund_id={refund_id}`

**Method** : `GET`

**Auth required** : NO

## Request

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| refund_id | string | Yes | Refund ID from create refund response  / ID инвойса из ответа создания возврата |

```
GET /payment/one_qr/refund/status?refund_id=REFF5149C4B458F4D7FB
```

## Response

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.refund_id | string | Refund ID / ID возврата |
| data.status | integer | Payment status: 1=in pending, 2=success, 3=failed / Статус оплаты |

**Success example — payment completed**

**Code** : `200 OK`

```json
{
  "data": {
    "refund_id": "REFF5149C4B458F4D7FB",
    "status": 2
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
    "refund_id": "REFF5149C4B458F4D7FB",
    "status": 1
  },
  "error": null,
  "is_success": true
}
```

**Success example — payment declined**

**Code** : `200 OK`

```json
{
  "data": {
    "refund_id": "REFF5149C4B458F4D7FB",
    "status": 3
  },
  "error": null,
  "is_success": true
}
```

**Error example**

**Code** : `200 OK`

```json
{
    "data": null,
    "error": {
        "code": 9001,
        "message": "Временная ошибка UzQR. Повторите позже.",
        "data": null
    },
    "is_success": false
}
```
