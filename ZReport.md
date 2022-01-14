# ZREPORT

## Open ZReport
Operation for open ZReport / Открытие кассовой смены

**URL** : `/zreport/open/`

**Method** : `GET`

**Parameter** : `time [in format yyyy-MM-dd HH:mm:ss]`

**Auth required** : NO

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

**Parameter** : `time [in format yyyy-MM-dd HH:mm:ss]`

**Auth required** : NO

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
  "total_refund_vat": [ZReport refund NDS price multiplied by 100]
  "total_refund_card": [ZReport refund card price multiplied by 100]
  "total_refund_cash": [ZReport refund cash price multiplied by 100]
  "total_refund_count": [ZReport refund count] ,
  "total_sale_vat": [ZReport sale NDS price multiplied by 100],
  "total_sale_card": [ZReport sale card price multiplied by 100]
  "total_sale_cash": [ZReport sale cash price multiplied by 100]
  "total_sale_count": [ZReport sale count] ,
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

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
      "total_sale_count": 0
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

## Close ZReport with print (X report = "false")
Operation for close ZReport / Закрытие кассовой смены с напечатыванием чека 

**URL** : `/zreport/close/`

**Method** : `POST`

**Parameter** : `time [in format yyyy-MM-dd HH:mm:ss]`

**Auth required** : NO

## Request
```json
{
"close_zreport": [Close zreport true or false]
 "name": [zreport name], 
 "prices":[
  {
    "name":[Price name {UZS,USD,HUMO}]
    "price":[price  multiplied by 100]
  }
 ]
}
```
**Data example**

```
{
"close_zreport": true,
"name":"Z Отчет",
"prices":[
  {
   "name":"UZS",
   "price":240000
   }
 ]
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
  "total_refund_vat": [ZReport refund NDS price multiplied by 100]
  "total_refund_card": [ZReport refund card price multiplied by 100]
  "total_refund_cash": [ZReport refund cash price multiplied by 100]
  "total_refund_count": [ZReport refund count] ,
  "total_sale_vat": [ZReport sale NDS price multiplied by 100],
  "total_sale_card": [ZReport sale card price multiplied by 100]
  "total_sale_cash": [ZReport sale cash price multiplied by 100]
  "total_sale_count": [ZReport sale count] ,
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

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
      "total_sale_count": 3
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

## ZReport Info
Operation for ZReport Info / Проверка состояния кассовой смены

**URL** : `/zreport/info/`

**Method** : `GET`

**Auth required** : NO

## Response

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
      "total_sale_count": 0
    },
    "error": null,
    "is_success": true
  }
}
```
| Name                        | Type   | Description EN/RU                                                      | Example                                    |
| --------------------------- | -------| ---------------------------------------------------------------------- | ------------------------------------------ |
| applet_version              | String | Fiscal module applet version/Версия аплета фискального модуля          | 0302                                       |
| terminal_id                 | String | Fiscal module number/Номер фискального модуля                          | UZ191211501001                             |
| number                      | String | Number/Номер смены                                                     | 118                                        |
| count                       | String | Count/Кол-во закрытых смен                                             | 118                                        |
| last_receipt_seq            | String | Last receipt seq/Последний номер чека                                  | 1159                                       |
| first_receipt_seq           | String | First receipt seq/Первый номер чека в текущей смене                    | 1157                                       |
| open_time                   | String | Open time/Дата и время открытия смены                                  | 2022-01-14 10:43:00                        |
| close_time                  | String | Close time/Дата и время закрытия смены                                 | ""                                         |
| total_refund_vat            | String | Total refund vat/Сумма возврата НДС                                    | 0                                          |
| total_refund_card           | String | Total refund card/Сумма возврата по карте                              | 0                                          |
| total_refund_cash           | String | Total refund cash/Сумма вовзрата наличкой                              | 0                                          |
| total_refund_count          | String | Total refund count/Количество возвратных чеков                         | 0                                          |
| total_sale_vat              | String | Total sale vat/Сумма продаж НДС                                        | 0                                          |
| total_sale_card             | String | Total sale card/Сумма продаж по картам                                 | 0                                          |
| total_sale_cash             | String | Total sale cash/Сумма продаж наличкой                                  | 0                                          |
| total_sale_count            | String | Total sale count/Количество продажных чеков                            | 0                                          |
