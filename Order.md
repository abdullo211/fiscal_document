# ORDER

## Order create
Operation for create order / Продажа

**URL** : `/order/create/`

**Method** : `POST`

**Auth required** : NO

**Data constraints**
-- With * are optional fields
```json
{
"number":[*order number or id],
"products":
[
  {
   "name":[product name], 
   "barcode":[product barcode], 
   "amount":[product amount],
   "price":[product_price * amount],
   "product_price":[product_price], 
   "vat":[nds_price], 
   "vat_percent":[nds_percent],
   "discount":[discount_price],
   "discount_percent":[discount_price_percent],
   "other":[other_discount_prices  multiplied by 100],
  *"labels":[marking_codes_list],
  *"class_code":[product_class_code]
   }
], 
"time":[time_in_format yyyy-MM-dd HH:mm:ss],
"cashier":[cashier_name], 
"received_cash":[received_cash_price], 
"change":[change_price], 
"received_card":[received card price  multiplied by 100],
*"send_email":[Send order data to special email],
*"email":[Email for sending order data],
*"sms_phone_number" : [Phone number for sending order data],
*"open_cashbox":[open cashbox device],
*"banners":[
  {
    "type":[Banner type - {text, barcode, qr_code}]
    "data":[Banner text]
  }
 ],
*"prices":
[
  {
   "name":[price_name], 
   "price":[price], 
   "vat_type":[vat_name],
   "vat_price":[vat_price],
   }
] 
}
```

| Name               | Type   | Description EN/RU                                                              | Example                                     |
| ------------------ | -------| ------------------------------------------------------------------------------ | ------------------------------------------- |
| number             | String | Forder number/Номер чека                                                       | 1                                           |
| name               | String | Product name/Наименование товара или услуги                                    | Хлеб                                        |
| barcode            | String | Product barcode/Штрих-код (GTIN) товара                                        | EAN-8 47800007, EAN-13 4780000000007        |
| amount             | String | Product amount/Количество                                                      | 1 шт. = 1000; 0,25 кг = 250                 |
| price              | String | Price/Сумма                                                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| product_price      | String | Product price/Цена за единицу товара/услуги                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| vat                | String | Nds price/Сумма НДС                                                            | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| vat_percent        | String | Nds percent/Ставка НДС                                                         | 0 = 0%, 10 = 10%, 15 = 15%, 20 = 20%        |
| discount           | String | Discount price/Цена cкидки                                                     | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| discount_percent   | String | Discount price percent/Процент скидки                                          | 0 = 0%, 10 = 10%, 15 = 15%, 20 = 20%        |
| other              | String | Other discount prices/Другая скидка                                            | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| labels             | String | Marking codes list/Код маркировки (значеник кода DataMatrix)                   | 05367567230048c?eN1(o0029                   |
| class_code         | String | Product class code/Код классификатора ИКПУ                                     | 10999001001000000                           |
| time               | String | Time in format yyyy-MM-dd hh:mm:ss/Дата и время в формате yyyy-MM-dd hh-mm-ss  | 2021-09-08 22:54:59                         |
| cashier            | String | Cashier name/Имя кассира                                                       | Админ                                       |
| received_cash      | String | Received cash price/Оплата наличными                                           | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| change             | String | Change price/Сдача                                                             | 100                                         |
| received_card      | String | Received cash price/Оплата банковской картой                                   | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| open_cashbox       | String | Open cashbox device/Открытие денежнего ящика                                   | true = open, falce = not open               |
| type               | String | Banner type - {text, barcode, qr_code}/Штрих-код, QR-код                       | barcode                                     |
| data               | String | Banner text/Рекламный текст                                                    | Скидка на следующую покупку 5%              |
| prices / name      | String | Price name/Наименование вида оплаты                                            | UDS, VISA, MasterCard, ...                  |
| prices / price     | String | Price/Сумма                                                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| prices / vat_type  | String | Vat type/Название налога и ставка                                              | НДС 15%                                     |
| prices / vat_price | String | Vat price/Сумма налога                                                         | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |


**Data example**

```json
{
  "number":1, 
  "products":
  [
    {
     "name":"наименование товара или услуги", 
     "barcode":"4780000000007", 
     "amount":2000,
     "price":115000,
     "product_price":230000, 
     "vat":1500, 
     "vat_percent":15,
     "discount":115000,
     "discount_percent":50,
     "other":0,
     "labels":["05367567230048c?eN1(o0029","05367567230048b5Mp17W3346"],
     "class_code":"02206"
    }
  ], 
"time":"2021-04-07 12:52:02",
"cashier":"Admin", 
"received_cash":100000, 
"change":0, 
"received_card":15000,
"open_cashbox":true,
"send_email":true,
"email":"abdullo21113@gmail.com",
"sms_phone_number" :"+998909999999",
"banners":
[ 
  {
  "type":"text",
  "data": "Код скидки для следующий покупки "
  },
  {
  "type":"barcode",
  "data":"23423423"
  }
],
"prices":
  [
    {
     "name":"PayMe", 
     "price":100000,
     "vat_type":"QQS", 
     "vat_price":200000
    }
  ], 
}
 }
```

## Response

```json
{
 "data":{
  "terminal_id": [id of terminal ], 
  "receipt_count": [receipt count int zreport],
  "date_time": [Date time in tm],
  "fiscal_sign": [fiscal sign number], 
  "applet_version": [version of applet], 
  "qr_url": [qrcode url],
  "cash_box_number": [cashbox number]
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

| Name           | Type   | Description EN/RU                                                   | Example                                                         |
| -------------- | -------| ------------------------------------------------------------------- | --------------------------------------------------------------- |
| terminal_id    | String | Fiscal module number/Номер фискального модуля                       | UZ170703100189                                                  |
| receipt_count  | String | Receipt count/Номер чека                                            | 643                                                             |
| date_time      | String | Date in format YYYYMMDDHHMMSS/Дата и время в формате ГГГГММДДЧЧММСС | 20200518221403                                                  |
| fiscal_sign    | String | Fiscal sign/Фискальный признак                                      | 248429044289                                                    |
| applet_version | String | Applet version/Версия аплета                                        | 0300                                                            |
| qr_url         | String | QR url/QR ссылка                                                    | https://ofd.soliq.uz/check?t=UZ170703100189&r=643&c=20200518221 |

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
"data": {
  "terminal_id": "UZ170703100189", 
  "receipt_count": 643,
  "date_time": "20200518221403",
  "fiscal_sign": "248429044289", 
  "applet_version": "0300", 
  "qr_url": "https://ofd.soliq.uz/check?t=UZ170703100189&r=643&c=20200518221403&s=248429044289" 
  },
"error": null,
"is_success": true 
}
```
**Error example**
**Condition** : If 'Printer not working'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 101 ,
    "message": "Printer not working",
    "data": null
    },
"is_success": false 
}
```


## Order refuse
Operations for refuse order / Возврат

**URL** : `/order/refuse/`

**Method** : `POST`

**Auth required** : NO

**Data constraints**

```json
{
"number":[order number or id],
"products":
[
  {
   "name":[product name String], 
   "barcode":[product barcode String], 
   "amount":[product amount  multiplied to 1000],
   "price":[product_price * amount],
   "product_price":[product_price multiplied to 100], 
   "vat":[nds price multiplied to 100], 
   "vat_percent":[nds percent],
   "discount":[discount price  multiplied to 100],
   "discount_percent":[discount price percent],
   "other":[other discount prices  multiplied to 100] 
  *"labels":[marking codes list],
  *"class_code":[product class code for marking]
   }
], 
"time":[Time in format yyyy-MM-dd HH:mm:ss],
"cashier":[Cashier name], 
"received_cash":[received cash price  multiplied to 100], 
"change":[change price multiplied to 100], 
"received_card":[received card price  multiplied to 100],
*"send_email":[Send order data to special email],
*"email":[Email for sending order data],
*"sms_phone_number" : [Phone number for sending order data],
"prices":
[
  {
   "name":[price name String], 
   "price":[price multiplied by 100], 
   "vat_type":[vat name String],
   "vat_price":[vat price multiplied by 100],
   }
], 
}
```

**Data example**

```json
{
  "number":1, 
  "products":
  [
    {
     "name":"наименование товара или услуги", 
     "barcode":"4780000000007", 
     "amount":1000.0,
     "price":230000.0,
     "product_price":2300.0, 
     "vat":15000.0, 
     "vat_percent":15,
     "discount":115000.0,
     "discount_percent":50.0,
     "other":0.0,
     "labels":["05367567230048c?eN1(o0029","05367567230048b5Mp17W3346"],
     "class_code":"02206"
    }
  ], 
"time":"2021-04-15 14:35:02",
"cashier":"Admin", 
"received_cash":100000, 
"change":0, 
"send_email":true,
"email":"abdullo21113@gmail.com",
"sms_phone_number" :"+998909999999",
"received_card":15000,
"prices":
  [
    {
     "name":"UPAY", 
     "price":100000,
     "vat_type":"TUZATISH QQS", 
     "vat_price":200000
    }
  ], 
}
}
```

## Response

```json
 {
 "data":{
  "terminal_id": [id of terminal ], 
  "receipt_count": [receipt count int zreport],
  "date_time": [Date time in tm],
  "fiscal_sign": [fiscal sign number], 
  "applet_version": [version of applet], 
  "qr_url": [qrcode url]
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
"data": {
  "terminal_id": "UZ170703100189", 
  "receipt_count": 643,
  "date_time": "20200518221403",
  "fiscal_sign": "248429044289", 
  "applet_version": "0300", 
  "qr_url": "https://ofd.soliq.uz/check?t=UZ170703100189&r=643&c=20200518221403&s=248429044289",
  "cash_box_number":"2"
  },
"error": null,
"is_success": true 
}
```
**Error example**
**Condition** : If 'Fiscal module is not initialized yet'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
 "error": {
    "code": 102,
    "message": "FISCAL_MODULE_NOT_INITIALIZED",
    "data": null
    },
"is_success": false 
}
```




## Order print
Operation for print last order / Печать последнего чека

**URL** : `/order/print/`

**Method** : `GET`

**Auth required** : NO

## Response

```json
 {
 "data":null,
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
"data": null,
"error":null,
"is_success": true 
}
```

**Error example**
**Condition** : If 'Printer not working'
**Code** : `200 OK`

**Content** :
```json
{
"data": null,
"error": {
    "code": 101,
    "message": "Printer not working",
    "data": null
    },
"is_success": false 
}
```


