# Humo / Оплата через терминал (Ingenico iPP 320, Lane 3000, Lane 7000) Humo

Operation for create paymen via Humo PinPad

**URL** : `/payment/xumo`

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
