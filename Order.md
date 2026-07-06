# ORDER

## Order create
Operation for create order / Продажа, аванс, кредит

**URL** : `/order/create/`

**Method** : `POST`

**Auth required** : NO

**Data constraints**
-- With * are optional fields / Поля опциональные. Для более подробной информации обращаться в телеграм группу
Если нужна интеграция с Payme,Click,Uzum, то поле extra_info считается обязательным
```json
{
"number":[*order number or id],
"receipt_type":[receipt_type],
"products":
[
  {
   "name":[product name],
   "barcode":[product barcode], 
   "amount":[product amount multiplied by 1000],
   "unit_name":[unit name],
   "price":[product_price * amount multiplied by 100],
   "product_price":[product_price multiplied by 100], 
   "vat":[nds_price multiplied by 100], 
   "vat_percent":[nds_percent],
   "discount":[discount_price multiplied by 100],
   "discount_percent":[discount_price_percent number],
   "other":[other_payments  multiplied by 100],
   "labels":[marking_codes_list],
   "class_code":[product_class_code],
   "package_code":[package_code string],
   "owner_type":[owner_type],
   "comission_info":{
              "inn":"inn comision",
              "pinfl":"pinfl comision"
   }
   }
],
*"uuid":[your uuid number], 
"time":[time_in_format yyyy-MM-dd HH:mm:ss],
"cashier":[cashier_name], 
"received_cash":[received_cash_price multiplied by 100], 
"change":[change_price multiplied by 100], 
"received_card":[received card price  multiplied by 100],
"card_type":[card type personal (2) or corporate (1)],
"ppt_id":[ RRN number (ppt_id) in the slip response from the bank pinpad (Humo, Uzcard)],
*"scan2pay_paid":[If the payment was made through the service Scan2Pay true or false],
"extra_info":{
    *"phone_number":[Phone_number from response Payme,Click,Uzum],
    *"qr_payment_id":[Payment_ID from response Payme,Click,Uzum],
    *"qr_payment_provider":[provider code number: 141 - Payme, 64 - Click, 161 - Uzum, 187 - Anor bank],
    *"scan2pay_id":[uuid from /payment/qr_pay/status],
    *"card_number":[bank card number first 4 and last 4 digits for Social Card Type]
          },
*"send_email":[Send order data to special email],
*"email":[Email for sending order data],
*"sms_phone_number" : [Phone number for sending order data],
*"open_cashbox":[open cashbox device],
*"banners":[
  {
    "type":[Banner type - {text, barcode}]
    "data":[Banner text]
    "cut":[true or false]
    "style:{[Style text,barcode]
            "font_width":[font_width],
            "font_height":[font_height],
            "is_bold":[true or false],
            "align":[center, left, right],
            "barcode_type":[barcode type],
            "qr_size":[QR size]
  },
 ],
*"prices":
[
  {
   "name":[price_name],
   "type":[price_type],
   "price":[price], 
   "vat_type":[vat_name],
   "vat_price":[vat_price],
   }
] 
}
```

| Name               | Type           | Required | Description EN/RU                                                              | Example                                     |
| ------------------ | -------------- | -------- | ------------------------------------------------------------------------------ | ------------------------------------------- |
| number             | integer        | No       | Forder number/Номер чека                                                       | 1                                           |
| receipt_type       | string         | Yes      | Receipt type: `order`, `prepaid`, `credit` / Вид продажи. Note: QR and fiscal sign are not printed on prepaid and credit receipts / На авансовые и кредитные чеки QR и фиск.признак не печатается | order,prepaid,credit                        |
| name               | string         | Yes      | Product name/Наименование товара или услуги                                    | Хлеб                                        |
| barcode            | string         | No       | Product barcode/Штрих-код (GTIN) товара                                        | EAN-8 47800007, EAN-13 4780000000007        |
| amount             | integer        | Yes      | Product amount/Количество                                                      | 1 шт. = 1000; 0,25 кг = 250                 |
| unit_name          | string         | Yes      | Unit name for receipt (UZ latin) / Единица измерения на чеке. Values from tasnif.soliq.uz | dona                                        |
| price              | integer        | Yes      | Price/Сумма                                                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| product_price      | integer        | Yes      | Product price/Цена за единицу товара/услуги                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| vat                | integer        | No       | VAT price/Сумма НДС/ Расчет НДС (VAT calculate) Price*12/112                   | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| vat_percent        | integer        | No       | VAT percent/Процент НДС                                                        | 0 = 0%, 12 = 12%, null - БЕЗ НДС            |
| discount           | integer        | No       | Discount price/Цена cкидки                                                     | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| discount_percent   | number         | No       | Discount price percent/Процент скидки                                          | 0 = 0%, 10 = 10%, 15 = 15%, 20 = 20%        |
| other              | integer        | No       | Other payments (gift card)/Другая оплата (карта лояльности, подарочные карты)  | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| labels             | array\<string\> | No       | Marking codes (DataMatrix) / Коды маркировки. If quantity is 5 marked items, set `amount` to 1000 per unit (1 шт = 1000) | ["05367567230048c?eN1(o0029"]              |
| class_code         | string         | Yes      | Product class code/Код ИКПУ (МХИК) (tasnif.soliq.uz)                           | 10999001001000000                           |
| package_code       | string         | Yes      | Package_code/ Код ед.измерений / упаковки (tasnif.soliq.uz)                    | "1520627"                                   |
| owner_type         | integer        | Yes      | Product origin / Код происхождения: `0` — bought and sold (куплено и продано), `1` — own production (собственное производство), `2` — service provider (поставщик услуг) | 1                                           |
| comission_info     | object         | No       | Sign commission check TIN, PINFL/Признак комиссионный чек ИНН, ПИНФЛ           | {"inn":"123456789","pinfl":"12345678912345"} |
| uuid               | string         | No       | Your UUID / Ваш UUID                                                           | abc123                                      |
| time               | string         | Yes      | Time in format yyyy-MM-dd HH:mm:ss/Дата и время в формате yyyy-MM-dd HH:mm:ss  | 2021-09-08 22:54:59                         |
| cashier            | string         | Yes      | Cashier name/Имя кассира                                                       | Админ                                       |
| received_cash      | integer        | Yes      | Received cash price/Оплата наличными                                           | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| change             | integer        | Yes      | Change price/Сдача                                                             | 100                                         |
| received_card      | integer        | Yes      | Received card price/Оплата банковской картой,Payme,Click,UZUM                  | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| card_type          | integer        | No       | Card type / Тип карты: `1` — corporate (корпоративная), `2` — personal (личная), `3` — social (социальная). For social card, also pass `extra_info.card_number` | 2                                           |
| ppt_id             | string         | No       | Номер RRN (ppt_id) в слипе ответе от банквоского пинпада (Humo, Uzcard)        | 123456789012                                |
| scan2pay_paid      | boolean        | No       | If the payment was made through the service Scan2Pay true or false             | true or false                               |
| scan2pay_id        | string         | No       | uuid from /payment/qr_pay/status / uuid из /payment/qr_pay/status              | 59bcc56b-1fcf-4752-9f5b-a3fffdf525ae        |
| extra_info         | object         | Cond.    | Required for Payme/Click/Uzum integration/Обязательно для интеграции с ЭПС     |                                             |
| extra_info.phone_number | string    | No       | Phone from payment response/Телефон из ответа оплаты                           | 998911234569                                |
| extra_info.qr_payment_id | string   | No       | Payment ID from provider/ID оплаты от провайдера                               | 123456789id12                               |
| extra_info.qr_payment_provider | integer | No  | Provider code number: 141 Payme, 64 Click, 161 Uzum, 187 Anor/Код провайдера   | 141                                         |
| extra_info.card_number | string     | No       | Card number for social card type/Номер карты для социальной карты              | 1234********1234                            |
| open_cashbox       | boolean        | No       | Open cashbox device/Открытие денежного ящика                                   | true = open, false = not open               |
| send_email         | boolean        | No       | Send order data to special email/Отправка данных на email                      | true                                        |
| email              | string         | No       | Email for sending order data/Email для отправки данных                         | user@example.com                            |
| sms_phone_number   | string         | No       | Phone number for sending order data/Телефон для отправки данных              | +998909999999                               |
| type               | string         | No       | Banner type - {text, barcode, qr_code}/Штрих-код, QR-код                       | barcode                                     |
| data               | string         | No       | Banner text/Рекламный текст                                                    | Скидка на следующую покупку 5%              |
| cut                | boolean        | No       | Cut receipt after banner/Отрезать чек после баннера                            | false                                       |
| style.font_width   | integer        | No       | Banner font width/Ширина шрифта баннера                                        | 2                                           |
| style.font_height  | integer        | No       | Banner font height/Высота шрифта баннера                                       | 100                                         |
| style.is_bold      | boolean        | No       | Banner bold flag/Жирный шрифт баннера                                          | true                                        |
| style.align        | string         | No       | Banner alignment: `center`, `left`, `right`/Выравнивание баннера               | center                                      |
| style.barcode_type | integer        | No       | Barcode type/Тип штрих-кода                                                    | 0                                           |
| style.qr_size      | integer        | No       | QR code size/Размер QR-кода                                                    | 5                                           |
| prices / name      | string         | No       | Price name/Наименование вида оплаты                                            | USD, VISA, MasterCard, Click, Payme, Uzum   |
| prices / type      | string         | No       | Price type/Тип оплаты                                                          | card                                        |
| prices / price     | integer        | No       | Price/Сумма                                                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| prices / vat_type  | string         | No       | Vat type/Название налога и ставка                                              | НДС 15%                                     |
| prices / vat_price | integer        | No       | Vat price/Сумма налога                                                         | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |



**Data example**

```json
{
  "number": 1,
  "receipt_type": "order",
  "products": [
    {
      "name": "наименование товара или услуги",
      "barcode": "4780000000007",
      "amount": 1000,
      "unit_name": "litr",
      "price": 50000,
      "product_price": 50000,
      "vat": 6000,
      "vat_percent": 12,
      "discount": 0,
      "discount_percent": 0,
      "other": 0,
      "labels": ["05367567230048c?eN1(o0029"],
      "class_code": "02710001005000000",
      "package_code": "1282556",
      "owner_type": 1,
      "comission_info": {
        "inn": "123456789",
        "pinfl": "12345678912345"
      }
    }
  ],
  "uuid": "123",
  "time": "2021-04-07 12:52:02",
  "cashier": "Admin",
  "received_cash": 50000,
  "change": 0,
  "received_card": 0,
  "card_type": 2,
  "ppt_id": "123456789012",
  "scan2pay_paid": true,
  "extra_info": {
    "phone_number": "998911234569",
    "qr_payment_id": "123456789id12",
    "qr_payment_provider": 141,
    "scan2pay_id": "59bcc56b-1fcf-4752-9f5b-a3fffdf525ae",
    "card_number": "1234********1234"
  },
  "open_cashbox": true,
  "send_email": true,
  "email": "abdullo21113@gmail.com",
  "sms_phone_number": "+998909999999",
  "banners": [
    {
      "type": "text",
      "data": "Код скидки для следующий покупки",
      "cut": false,
      "style": {
        "font_width": 2,
        "font_height": 100,
        "is_bold": true,
        "align": "center",
        "barcode_type": 0,
        "qr_size": 5
      }
    },
    {
      "type": "barcode",
      "data": "23423423",
      "cut": false,
      "style": {
        "font_width": 2,
        "font_height": 100,
        "is_bold": true,
        "align": "center",
        "barcode_type": 0,
        "qr_size": 5
      }
    }
  ],
  "prices": [
    {
      "name": "PayMe",
      "type": "card",
      "price": 100000,
      "vat_type": "QQS",
      "vat_price": 200000
    }
  ]
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

| Name           | Type    | Required | Description EN/RU                                                   | Example                                                         |
| -------------- | ------- | -------- | ------------------------------------------------------------------- | --------------------------------------------------------------- |
| terminal_id    | string  | Yes      | Fiscal module number/Номер фискального модуля                       | UZ170703100189                                                  |
| receipt_count  | integer | Yes      | Receipt count/Номер чека                                            | 643                                                             |
| date_time      | string  | Yes      | Date in format YYYYMMDDHHMMSS/Дата и время в формате ГГГГММДДЧЧММСС | 20200518221403                                                  |
| fiscal_sign    | string  | Yes      | Fiscal sign/Фискальный признак                                      | 248429044289                                                    |
| applet_version | string  | Yes      | Applet version/Версия аплета                                        | 0300                                                            |
| qr_url         | string  | Yes      | QR url/QR ссылка                                                    | https://ofd.soliq.uz/check?t=UZ170703100189&r=643&c=20200518221 |
| cash_box_number| string  | No       | Cashbox number/Номер денежного ящика                                | 2                                                               |
| is_success     | boolean | Yes      | Success flag/Признак успешного ответа                               | true                                                            |
| error.code     | integer | No       | Error code/Код ошибки                                               | 101                                                             |

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
   "unit_name":[unit name],
   "price":[product_price * amount],
   "product_price":[product_price multiplied to 100], 
   "vat":[nds price multiplied to 100], 
   "vat_percent":[nds percent],
   "discount":[discount price  multiplied to 100],
   "discount_percent":[discount price percent number],
   "other":[other discount prices  multiplied to 100],
   "class_code":[product class code for marking],
  *"labels":[marking codes list],
   "package_code":[package_code string],
   "owner_type":[owner_type],
   "comission_info":{
              "inn":"inn/pinfl comision"
   }
  
   }
],
*"uuid":[your uuid number],
"qr_code":[link to web],
"time":[Time in format yyyy-MM-dd HH:mm:ss],
"cashier":[Cashier name], 
"received_cash":[received cash price  multiplied to 100], 
"change":[change price multiplied to 100], 
"received_card":[received card price  multiplied to 100],
"card_type":2,
"ppt_id":"123456789012",
"extra_info":{
    *"phone_number":"998911234569",
    *"qr_payment_id":"123456789id12"
    *"qr_payment_provider":[provider code number]
          },
*"send_email":[Send order data to special email],
*"email":[Email for sending order data],
*"sms_phone_number" : [Phone number for sending order data],
"prices":
[
  {
   "name":[price name String],
   "type":[price type String],
   "price":[price multiplied by 100], 
   "vat_type":[vat name String],
   "vat_price":[vat price multiplied by 100],
   }
], 
}
```

| Field | Type | Required | Description EN/RU |
| ----- | ---- | -------- | ----------------- |
| number | integer | Yes | Order number/Номер чека |
| products | array | Yes | Product list/Список товаров (same fields as `/order/create/`) |
| qr_code | string | Yes | Original receipt URL/URL исходного чека для возврата |
| time | string | Yes | Time `yyyy-MM-dd HH:mm:ss`/Дата и время |
| cashier | string | Yes | Cashier name/Имя кассира |
| received_cash | integer | Yes | Cash refund amount (×100)/Сумма возврата наличными |
| change | integer | Yes | Change amount (×100)/Сдача |
| received_card | integer | Yes | Card refund amount (×100)/Сумма возврата по карте |
| card_type | integer | No | Card type/Тип карты |
| ppt_id | string | No | RRN from pinpad/RRN с пинпада |
| extra_info | object | No | Payment provider info/Данные ЭПС |
| uuid | string | No | Your UUID/Ваш UUID |
| send_email | boolean | No | Send to email/Отправка на email |
| email | string | No | Email address/Email |
| sms_phone_number | string | No | SMS phone/Телефон для SMS |
| prices | array | No | Payment breakdown/Разбивка оплат |

**Data example**

```json
{
  "number": 1,
  "products": [
    {
      "name": "наименование товара или услуги",
      "barcode": "4780000000007",
      "amount": 1000,
      "unit_name": "dona",
      "price": 230000,
      "product_price": 230000,
      "vat": 15000,
      "vat_percent": 12,
      "discount": 115000,
      "discount_percent": 50,
      "other": 0,
      "labels": ["05367567230048c?eN1(o0029"],
      "class_code": "04811001001000000",
      "package_code": "1431970",
      "owner_type": 1,
      "comission_info": {
        "inn": "123456789",
        "pinfl": "12345678912345"
      }
    }
  ],
  "uuid": "123",
  "qr_code": "https://ofd.soliq.uz/check?t=UZ191211501001&r=1447&c=20220309125810&s=461313663448",
  "time": "2021-04-15 14:35:02",
  "cashier": "Admin",
  "received_cash": 100000,
  "change": 0,
  "received_card": 15000,
  "card_type": 2,
  "ppt_id": "123456789012",
  "extra_info": {
    "phone_number": "998911234569",
    "qr_payment_id": "123456789id12",
    "qr_payment_provider": 141
  },
  "send_email": true,
  "email": "abdullo21113@gmail.com",
  "sms_phone_number": "+998909999999",
  "prices": [
    {
      "name": "UPAY",
      "type": "card",
      "price": 100000,
      "vat_type": "TUZATISH QQS",
      "vat_price": 200000
    }
  ]
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

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| terminal_id | string | Fiscal module number/Номер фискального модуля |
| receipt_count | integer | Receipt number/Номер чека |
| date_time | string | Date-time `YYYYMMDDHHMMSS`/Дата и время |
| fiscal_sign | string | Fiscal sign/Фискальный признак |
| applet_version | string | Applet version/Версия аплета |
| qr_url | string | QR receipt URL/QR ссылка на чек |
| cash_box_number | string | Cashbox number/Номер денежного ящика |
| is_success | boolean | Success flag/Признак успешного ответа |
| error.code | integer | Error code/Код ошибки |

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
**Condition** : If 'Refund info is not valid'
**Code** : `65275 OK`

**Content** :
```json
{
    "data": null,
    "error": {
        "code": 65275,
        "message": "not valid refund info",
        "data": "refund info is not valid"
    },
    "is_success": false
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
**Error example**
**Condition** : If 'Сannot encode receipt'
**Code** : `65531 OK`

**Content** :
```json
{
    "data": null,
    "error": {
        "code": 65531,
        "message": "cannot encode receipt",
        "data": "failed to make total block\n difference 65000 between 50000 and 115000 is larger than 10000\n math error\n"
    },
    "is_success": false
}
```
**Error example**
**Condition** : If 'Not enough cash for refund'
**Code** : `36913 OK`

**Content** :
```json
{
    "data": null,
    "error": {
        "code": 36913,
        "message": "ERROR_NOT_ENOUGH_CASH_FOR_REFUND",
        "data": "ERROR_NOT_ENOUGH_CASH_FOR_REFUND\n ERROR_NOT_ENOUGH_CASH_FOR_REFUND\n"
    },
    "is_success": false
}
```




## Order print
Operation for print copy last order / Печать копии последнего чека 

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

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data | null | Always null on success/Всегда null при успехе |
| error | object or null | Error object/Объект ошибки |
| is_success | boolean | Success flag/Признак успешного ответа |

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

## Check last successful order 
Operation for check last successful order / Проверка последнего успешного чека 

**URL** : `/order/last/`

**Method** : `GET`

**Auth required** : NO

## Response

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| result.data.order | object | Last order details/Данные последнего чека |
| result.data.order.number | integer | Receipt number/Номер чека |
| result.data.order.cashier | string | Cashier name/Имя кассира |
| result.data.order.products | array | Product list/Список товаров |
| result.data.order.time | string | Order time/Дата и время чека |
| result.data.order.received_cash | integer | Cash amount/Оплата наличными |
| result.data.order.received_card | integer | Card amount/Оплата картой |
| result.data.order.change | integer | Change/Сдача |
| result.data.order.open_cashbox | boolean | Cashbox opened/Денежный ящик открыт |
| result.data.order.receipt_type | string | Receipt type/Тип чека |
| result.data.order.card_type | integer | Card type/Тип карты |
| result.data.order.ppt_id | string | RRN/RRN операции |
| result.data.order.result_url | string | Fiscal receipt URL/URL фискального чека |
| result.data.order.scan2pay_paid | boolean | Scan2Pay payment flag/Оплата через Scan2Pay |
| result.data.result.TerminalID | string | Terminal ID/Номер фискального модуля |
| result.data.result.ReceiptSeq | integer | Receipt sequence/Номер чека в смене |
| result.data.result.DateTime | string | Fiscal date-time/Дата и время фискализации |
| result.data.result.FiscalSign | string | Fiscal sign/Фискальный признак |
| result.data.result.QRCodeURL | string | QR URL/QR ссылка |
| result.data.isRefund | boolean | Is refund receipt/Признак возвратного чека |
| result.is_success | boolean | Success flag/Признак успешного ответа |

```json
{
  "result": {
    "data": {
      "order": {
        "id": 0,
        "number": 142632,
        "cashier": "Abduraxmon",
        "products": [
          {
            "name": "armia 1",
            "barcode": "",
            "amount": 200,
            "product_price": 2500000000,
            "price": 2500000000,
            "vat": 1071,
            "vat_percent": 12,
            "discount_percent": 0.0,
            "discount": 0,
            "other": 0,
            "labels": [
              "12abb3"
            ],
            "class_code": "11199008003000001",
            "comission_info": {
              "TIN": "",
              "PINFL": ""
            },
            "unit_name": "dona",
            "package_code": "1506986",
            "owner_type": 1
          },
          {
            "name": "Настенный громкоговоритель динамик 3 дюйма цвет черный OVO3T-BL",
            "barcode": "",
            "amount": 200,
            "product_price": 2000000000,
            "price": 2000000000,
            "vat": 1071,
            "vat_percent": 12,
            "discount_percent": 0.0,
            "discount": 0,
            "other": 0,
            "labels": [
              "45242sdsf"
            ],
            "class_code": "11199008003000001",
            "comission_info": {
              "TIN": "",
              "PINFL": ""
            },
            "unit_name": "dona",
            "package_code": "1500169",
            "owner_type": 1
          }
        ],
        "time": "2026-04-15 10:40:06",
        "received_cash": 0,
        "received_card": 4500000000,
        "received_ecash": null,
        "change": 0,
        "open_cashbox": false,
        "banners": [
          {
            "type": "text",
            "data": "PRACUJ Z NAMI \r\n ",
            "cut": false,
            "style": {
              "font_height": 150,
              "font_width": 1,
              "is_bold": true,
              "align": "center",
              "barcode_type": 0,
              "qr_size": 5
            }
          },
          {
            "type": "qr_code",
            "data": "http://lpp.com.kariera/salony",
            "cut": false,
            "style": {
              "font_height": 200,
              "font_width": 2,
              "is_bold": true,
              "align": null,
              "barcode_type": 0,
              "qr_size": 12
            }
          },
          {
            "type": "text",
            "data": "LPP.COM/KARIERA/SALONY",
            "cut": false,
            "style": {
              "font_height": 150,
              "font_width": 1,
              "is_bold": true,
              "align": "center",
              "barcode_type": 0,
              "qr_size": 5
            }
          }
        ],
        "prices": [
          {
            "name": "TEXT A",
            "type": null,
            "price": 1000,
            "vat_type": null,
            "vat_price": null
          },
          {
            "name": "TEXT B",
            "type": null,
            "price": 1000,
            "vat_type": null,
            "vat_price": null
          }
        ],
        "isSynced": false,
        "type": "order",
        "cash_desc_serial": null,
        "cash_desc_number": null,
        "market_name": null,
        "inn": null,
        "email": "",
        "send_email": false,
        "sms_phone_number": "",
        "result_url": "https://ofd.soliq.uz/check?t=LG230110007813&r=2478&c=20260415104006&s=322032313241",
        "location": {
          "Latitude": 41.299123,
          "Longitude": 69.272375
        },
        "receipt_type": "order",
        "extra_info": {
          "Other": null,
          "PhoneNumber": "",
          "PINFL": "",
          "TIN": "",
          "CarNumber": "",
          "CardNumber": "9842********1078",
          "QrPaymentID": "",
          "QrPaymentProvider": null,
          "CardType": null,
          "PPTID": null,
          "scan2pay_id": ""
        },
        "qr_code": "",
        "special_print": false,
        "payment_id": null,
        "scan2pay_paid": false,
        "taxi_info": null,
        "merchant_info": null,
        "card_type": 3,
        "ppt_id": "603614527232",
        "dbId": 0,
        "uuid": ""
      },
      "fiscalOrder": null,
      "result": {
        "TerminalID": "LG230110007813",
        "ReceiptSeq": 2478,
        "DateTime": "20260415104006",
        "FiscalSign": "322032313241",
        "AppletVersion": "0323",
        "QRCodeURL": "https://ofd.soliq.uz/check?t=LG230110007813&r=2478&c=20260415104006&s=322032313241",
        "cash_box_number": "2"
      },
      "isRefund": false
    },
    "error": null,
    "is_success": true
  }
}
```
