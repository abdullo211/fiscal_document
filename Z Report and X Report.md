# Z REPORT and X Report

## Open ZReport
Operation for open ZReport / Открытие кассовой смены

**URL** : `/zreport/open/`

**Method** : `GET`

**Parameter** : `time` — string, format `yyyy-MM-dd HH:mm:ss`

**Auth required** : NO

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| time | string | Yes | Open time in format `yyyy-MM-dd HH:mm:ss`/Время открытия смены |

## Response

```json
{
 "data":{
  "time": [time open zreport], 
  "applet_version": [Applet version],
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.time | string | Z-report open time/Время открытия смены |
| data.applet_version | string | Applet version/Версия аплета |
| error.code | integer | Error code/Код ошибки |
| error.message | string | Error message/Сообщение об ошибке |
| is_success | boolean | Success flag/Признак успешного ответа |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
"data":{
  "time": "2020-04-24 13:01:02", 
  "applet_version": "0300",
  },
"error": null,
"is_success": true 
}
```
**Error example**
**Condition** : If 'ZReport is already open'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 9327,
    "message": "ZREPORT_ALREADY_OPEN",
    "data": null
    },
"is_success": false 
}
```
## Close ZReport
Operation for close ZReport / Закрытие кассовой смены

**URL** : `/zreport/close/`

**Method** : `GET`

**Parameter** : `time` — string, format `yyyy-MM-dd HH:mm:ss`

**Auth required** : NO

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| time | string | Yes | Close time in format `yyyy-MM-dd HH:mm:ss`/Время закрытия смены |

## Response

```json
{
  "data":{ 
  "applet_version": [Applet version],
  "terminal_id": [Terminal id],
  "number": [Number of ZReport],
  "count": [All ZReport count],
  "last_receipt_seq": [Last receipt number in this ZReport],
  "first_receipt_seq": [First receipt number in this ZReport],
  "open_time": [ZReport open time in format yyyy-MM-dd HH:mm:ss],
  "close_time": [ZReport close time in format yyyy-MM-dd HH:mm:ss],
  "total_refund_vat": [ZReport refund NDS price multiplied by 100],
  "total_refund_card": [ZReport refund card price multiplied by 100],
  "total_refund_cash": [ZReport refund cash price multiplied by 100],
  "total_refund_count": [ZReport refund count],
  "total_sale_vat": [ZReport sale NDS price multiplied by 100],
  "total_sale_card": [ZReport sale card price multiplied by 100],
  "total_sale_cash": [ZReport sale cash price multiplied by 100],
  "total_sale_count": [ZReport sale count],
  "shift_opened": [shift opened status],
  "cash_desc_serial": [cash descriptor serial],
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.applet_version | string | Applet version/Версия аплета |
| data.terminal_id | string | Terminal ID/Номер фискального модуля |
| data.number | integer | Z-report number/Номер смены |
| data.count | integer | Total closed shifts count/Кол-во закрытых смен |
| data.last_receipt_seq | integer | Last receipt number/Последний номер чека |
| data.first_receipt_seq | integer | First receipt number/Первый номер чека в смене |
| data.open_time | string | Shift open time/Время открытия смены |
| data.close_time | string | Shift close time/Время закрытия смены |
| data.total_refund_vat | integer | Refund VAT total (×100)/Сумма возврата НДС |
| data.total_refund_card | integer | Refund card total (×100)/Сумма возврата по карте |
| data.total_refund_cash | integer | Refund cash total (×100)/Сумма возврата наличными |
| data.total_refund_count | integer | Refund receipt count/Количество возвратных чеков |
| data.total_sale_vat | integer | Sale VAT total (×100)/Сумма продаж НДС |
| data.total_sale_card | integer | Sale card total (×100)/Сумма продаж по картам |
| data.total_sale_cash | integer | Sale cash total (×100)/Сумма продаж наличными |
| data.total_sale_count | integer | Sale receipt count/Количество продажных чеков |
| data.shift_opened | boolean | Shift opened status/Статус открытой смены |
| data.cash_desc_serial | string or null | Cash descriptor serial/Серийный номер кассы |
| is_success | boolean | Success flag/Признак успешного ответа |

**Success example**
**Code** : `200 OK`

**Content** :
```{
  "result": {
    "data": {
      "applet_version": "0300",
      "terminal_id": "UZ170703100597",
      "number": 17,
      "count": 17,
      "last_receipt_seq": 0,
      "first_receipt_seq": 0,
      "open_time": "2020-08-04 14:03:02",
      "close_time": "",
      "total_refund_vat": 0,
      "total_refund_card": 0,
      "total_refund_cash": 0,
      "total_refund_count": 0,
      "total_sale_vat": 0,
      "total_sale_card": 0,
      "total_sale_cash": 0,
      "total_sale_count": 0,
      "shift_opened": false,
      "cash_desc_serial": null
    },
    "error": null,
    "is_success": true
  }
}
```
**Error example**
**Condition** : If 'ZReport already closed'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 9326,
    "message": "ZREPORT_ALREADY_CLOSE",
    "data": null
    },
"is_success": false 
}
```

## Close ZReport with print (X report = "close_zreport": false)
Operation for close ZReport / Закрытие кассовой смены с напечатыванием чека / X report add inside body "close_zreport": false / Х отчет добавить внутри тела "close_zreport": false

**URL** : `/zreport/close/`

**Method** : `POST`

**Parameter** : `time` — string, format `yyyy-MM-dd HH:mm:ss`

**Auth required** : NO

| Parameter | Type | Required | Description EN/RU |
| --------- | ---- | -------- | ----------------- |
| time | string | Yes | Close time in format `yyyy-MM-dd HH:mm:ss`/Время закрытия смены |

## Request
```json
{
  "close_zreport": [Close zreport true or false],
  "name": [zreport name],
  "prices": [
    {
      "name": [Price name {UZS,USD,HUMO}],
      "type": [price type],
      "price": [price multiplied by 100],
      "vat_type": [VAT name],
      "vat_price": [VAT price multiplied by 100]
    }
  ],
  "banners": [banner objects]
}
```

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| close_zreport | boolean | Yes | Close shift (`true`) or X-report only (`false`)/Закрыть смену или только X-отчёт |
| name | string | No | Report title/Название отчёта |
| prices[].name | string | No | Currency or payment type name/Название валюты или вида оплаты |
| prices[].type | string | No | Price type/Тип оплаты |
| prices[].price | integer | No | Amount multiplied by 100/Сумма × 100 |
| prices[].vat_type | string | No | VAT type/Название налога и ставка |
| prices[].vat_price | integer | No | VAT amount multiplied by 100/Сумма налога × 100 |
| banners | array | No | Banners to print with report/Баннеры для печати с отчётом |

**Data example**

```json
{
  "close_zreport": true,
  "name": "Z Отчет",
  "prices": [
    {
      "name": "UZS",
      "type": "cash",
      "price": 240000,
      "vat_type": "QQS",
      "vat_price": 0
    }
  ],
  "banners": []
}
```


## Response

```json
{
 "data":{ 
  "applet_version": [Applet version],
  "terminal_id": [Terminal id],
  "number": [Number of ZReport],
  "count": [All ZReport count],
  "last_receipt_seq": [Last receipt number in this ZReport],
  "first_receipt_seq": [First receipt number in this ZReport],
  "open_time": [ZReport open time in format yyyy-MM-dd HH:mm:ss],
  "close_time": [ZReport close time in format yyyy-MM-dd HH:mm:ss],
  "total_refund_vat": [ZReport refund NDS price multiplied by 100],
  "total_refund_card": [ZReport refund card price multiplied by 100],
  "total_refund_cash": [ZReport refund cash price multiplied by 100],
  "total_refund_count": [ZReport refund count],
  "total_sale_vat": [ZReport sale NDS price multiplied by 100],
  "total_sale_card": [ZReport sale card price multiplied by 100],
  "total_sale_cash": [ZReport sale cash price multiplied by 100],
  "total_sale_count": [ZReport sale count],
  "shift_opened": [shift opened status],
  "cash_desc_serial": [cash descriptor serial],
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.applet_version | string | Applet version/Версия аплета |
| data.terminal_id | string | Terminal ID/Номер фискального модуля |
| data.number | integer | Z-report number/Номер смены |
| data.count | integer | Total closed shifts count/Кол-во закрытых смен |
| data.last_receipt_seq | integer | Last receipt number/Последний номер чека |
| data.first_receipt_seq | integer | First receipt number/Первый номер чека в смене |
| data.open_time | string | Shift open time/Время открытия смены |
| data.close_time | string | Shift close time/Время закрытия смены |
| data.total_refund_vat | integer | Refund VAT total (×100)/Сумма возврата НДС |
| data.total_refund_card | integer | Refund card total (×100)/Сумма возврата по карте |
| data.total_refund_cash | integer | Refund cash total (×100)/Сумма возврата наличными |
| data.total_refund_count | integer | Refund receipt count/Количество возвратных чеков |
| data.total_sale_vat | integer | Sale VAT total (×100)/Сумма продаж НДС |
| data.total_sale_card | integer | Sale card total (×100)/Сумма продаж по картам |
| data.total_sale_cash | integer | Sale cash total (×100)/Сумма продаж наличными |
| data.total_sale_count | integer | Sale receipt count/Количество продажных чеков |
| data.shift_opened | boolean | Shift opened status/Статус открытой смены |
| data.cash_desc_serial | string or null | Cash descriptor serial/Серийный номер кассы |
| is_success | boolean | Success flag/Признак успешного ответа |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
 "result": {
    "data": {
      "applet_version": "0300",
      "terminal_id": "UZ170703100597",
      "number": 3,
      "count": 20,
      "last_receipt_seq": 20,
      "first_receipt_seq": 18,
      "open_time": "2019-10-07 17:07:52",
      "close_time": "2019-10-09 19:16:15",
      "total_refund_vat": 0,
      "total_refund_card": 0,
      "total_refund_cash": 0,
      "total_refund_count": 0,
      "total_sale_vat": 195000,
      "total_sale_card": 0,
      "total_sale_cash": 195000,
      "total_sale_count": 3,
      "shift_opened": false,
      "cash_desc_serial": null
    },
    "error": null,
    "is_success": true
  }
}
```
**Error example**
**Condition** : If 'ZReport already closed'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 9326,
    "message": "ZREPORT_ALREADY_CLOSE",
    "data": null
    },
"is_success": false 
}
```

## ZReport Info #
Operation for ZReport Info / Проверка состояния кассовой смены на 3 апплете 

**URL** : `/zreport/info/`

**Method** : `GET`

**Auth required** : NO

## Response 3 APPLET

```json
{
  "result": {
    "data": {
      "applet_version": [applet version],
      "terminal_id": [terminal id],
      "number": [number],
      "count": [count],
      "last_receipt_seq": [last receipt seq],
      "first_receipt_seq": [first receipt seq],
      "open_time": [open time],
      "close_time": [close time],
      "total_refund_vat": [total refund vat],
      "total_refund_card": [total refund card],
      "total_refund_cash": [total refund cash],
      "total_refund_count": [total refund count],
      "total_sale_vat": [total sale vat],
      "total_sale_card": [total sale card],
      "total_sale_cash": [total sale cash],
      "total_sale_count": [total sale count]
    },
    "error": [error],
    "is_success": [is success response]
  }
}
```

## Response 4 APPLET
```json
{
  "result": {
    "data": {
      "applet_version": [applet version],
      "terminal_id": [terminal id],
      "number": [number],
      "count": [count],
      "last_receipt_seq": [last receipt seq],
      "first_receipt_seq": [first receipt seq],
      "open_time": [open time],
      "close_time": [close time],
      "total_refund_vat": [total refund vat],
      "total_refund_card": [total refund card],
      "total_refund_cash": [total refund cash],
      "total_refund_count": [total refund count],
      "total_sale_vat": [total sale vat],
      "total_sale_card": [total sale card],
      "total_sale_cash": [total sale cash],
      "total_sale_count": [total sale count],
      "shift_opened": [shift opened status],
      "cash_desc_serial": [cash descriptor serial]
    },
    "error": [error],
    "is_success": [is success response]
  }
}
```


**Success example**
**Code** : `200 OK`

**Content** :
```json
{
  "result": {
    "data": {
      "applet_version": "0302",
      "terminal_id": "UZ191211501001",
      "number": 118,
      "count": 118,
      "last_receipt_seq": 1159,
      "first_receipt_seq": 1157,
      "open_time": "2022-01-14 10:43:00",
      "close_time": "",
      "total_refund_vat": 0,
      "total_refund_card": 0,
      "total_refund_cash": 0,
      "total_refund_count": 0,
      "total_sale_vat": 0,
      "total_sale_card": 0,
      "total_sale_cash": 0,
      "total_sale_count": 0,
      "shift_opened": true,
      "cash_desc_serial": null
    },
    "error": null,
    "is_success": true
  }
}
```
| Name                        | Type    | Description EN/RU                                                      | Example                                    |
| --------------------------- | ------- | ---------------------------------------------------------------------- | ------------------------------------------ |
| applet_version              | string  | Fiscal module applet version/Версия аплета фискального модуля          | 0302                                       |
| terminal_id                 | string  | Fiscal module number/Номер фискального модуля                          | UZ191211501001                             |
| number                      | integer | Number/Номер смены                                                     | 118                                        |
| count                       | integer | Count/Кол-во закрытых смен                                             | 118                                        |
| last_receipt_seq            | integer | Last receipt seq/Последний номер чека                                  | 1159                                       |
| first_receipt_seq           | integer | First receipt seq/Первый номер чека в текущей смене                    | 1157                                       |
| open_time                   | string  | Open time/Дата и время открытия смены                                  | 2022-01-14 10:43:00                        |
| close_time                  | string  | Close time/Дата и время закрытия смены                                 | ""                                         |
| total_refund_vat            | integer | Total refund vat/Сумма возврата НДС                                    | 0                                          |
| total_refund_card           | integer | Total refund card/Сумма возврата по карте                              | 0                                          |
| total_refund_cash           | integer | Total refund cash/Сумма вовзрата наличкой                              | 0                                          |
| total_refund_count          | integer | Total refund count/Количество возвратных чеков                         | 0                                          |
| total_sale_vat              | integer | Total sale vat/Сумма продаж НДС                                        | 0                                          |
| total_sale_card             | integer | Total sale card/Сумма продаж по картам                                 | 0                                          |
| total_sale_cash             | integer | Total sale cash/Сумма продаж наличкой                                  | 0                                          |
| total_sale_count            | integer | Total sale count/Количество продажных чеков                            | 0                                          |
| shift_opened                | boolean | Shift opened status (applet 4 only)/Статус открытой смены              | true                                       |
| cash_desc_serial            | string or null | Cash descriptor serial/Серийный номер кассы                       | null                                       |
| is_success                  | boolean | Success flag/Признак успешного ответа                                  | true                                       |

## Промежуточная сверка итогов на пинпадах Ingenico с последующей печатью
Intermediate verification of sales on Ingenico pinpads with subsequent printing / Промежуточная проверка продаж на пинпадах Ingenico с последующей печатью

**URL** : `/payment/xumo_shortreport/`

**Method** : `GET`

**Auth required** : NO

## Response

```json
{
  "data": {
    "message": "<printed report text>",
    "ppt_id": null
  },
  "error": null,
  "is_success": true
}
```

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Printed short report text/Текст краткого отчёта |
| data.ppt_id | string or null | RRN reference/RRN операции |
| is_success | boolean | Success flag/Признак успешного ответа |

## Промежуточная сверка итогов на пинпаде PAX A35 с последующей печатью
Intermediate verification of sales on PAX A35 pinpads with subsequent printing / Промежуточная проверка продаж на пинпаде PAX A35 с последующей печатью

**URL** : `/payment/uzcard_shortreport/`

**Method** : `GET`

**Auth required** : NO

## Response

```json
{
  "data": {
    "message": "           ОБЫЧНЫЙ ТОВАР\n
====================================\n
           Краткий отчет\n
                                    \n
====================================\n
       Эквайер: UZCARD-Local\n
           OOO TEST TIME\n
         Tashkent, Main str\n
====================================\n
Терминал:                   00000013\n
Дата:17/04/25         Время:17:06:36\n
====================================\n
====================================\n
    Тип карты: UZCARD-MASTERCARD\n
====================================\n
Оплата                (5) 900.00 UZS\n
====================================\n
            Общий итог:\n
====================================\n
Оплата                (5) 900.00 UZS\n
====================================\n
Итого:\n
Дебет:                    900.00 UZS\n
Кредит:                    -0.00 UZS\n
Отмены дебет:              -0.00 UZS\n
Отмены кредит:             +0.00 UZS\n
                          900.00 UZS\n
====================================\n
====================================\n
                                    \n
====================================\n
           Отчет окончен\n
====================================\n",
    "ppt_id": null
  },
  "error": null,
  "is_success": true
}
```

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data.message | string | Printed short report text/Текст краткого отчёта |
| data.ppt_id | string or null | RRN reference/RRN операции |
| is_success | boolean | Success flag/Признак успешного ответа |
