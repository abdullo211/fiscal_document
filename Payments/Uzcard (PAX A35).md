# UzCard / Оплата через терминал (PAX A35) UzCard

Operation for create paymen via UzCard PinPad

**URL** : `/payment/uzcard`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "amount": [Payment price * 100]
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
