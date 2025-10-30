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
   "discount_percent":[discount_price_percent],
   "other":[other_payments  multiplied by 100],
   "labels":[marking_codes_list],
   "class_code":[product_class_code],
   "package_code":[package_code],
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
    *"qr_payment_provider":[0141 - Payme, 0064 - Click, 0161 - Uzum, 0187 - Anor bank],
    *"scan2pay_id":[uuid from /payment/qr_pay/status]
          },
*"send_email":[Send order data to special email],
*"email":[Email for sending order data],
*"sms_phone_number" : [Phone number for sending order data],
*"open_cashbox":[open cashbox device],
*"banners":[
  {
    "type":[Banner type - {text, barcode}]
    "data":[Banner text]
    "style:{[Style text,barcode]
            "font_width":[font_width],
            "font_height":[font_height],
            "is_bold":[true or false] 
  },
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
| number             | Integer| Forder number/Номер чека                                                       | 1                                           |
| receipt_type       | String | Receipt type/Вид продажи (продажа,аванс,кредит)                                | order,prepaid,credit                        |
|                    |        | Примечание: На авансовые и кредитные чеки QR код и фиск.признак не печатается  |                                             |
| name               | String | Product name/Наименование товара или услуги                                    | Хлеб                                        |
| barcode            | Long   | Product barcode/Штрих-код (GTIN) товара                                        | EAN-8 47800007, EAN-13 4780000000007        |
| amount             | Long   | Product amount/Количество                                                      | 1 шт. = 1000; 0,25 кг = 250                 |
| unit_name          | String | Unit name/Едииница измерения для отображения на чеке на лат. UZ                | dona                                        |
|                    |        | Название единиц измерения взять с сайта tasnif.soliq.uz                        |                                             |
| price              | Long   | Price/Сумма                                                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| product_price      | Long   | Product price/Цена за единицу товара/услуги                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| vat                | Long   | VAT price/Сумма НДС/ Расчет НДС (VAT calculate) Price*12/112                   | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| vat_percent        | Integer| VAT percent/Процент НДС                                                        | 0 = 0%, 12 = 12%, null - БЕЗ НДС            |
| discount           | Long   | Discount price/Цена cкидки                                                     | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| discount_percent   | Integr | Discount price percent/Процент скидки                                          | 0 = 0%, 10 = 10%, 15 = 15%, 20 = 20%        |
| other              | Long   | Other payments (gift card)/Другая оплата (карта лояльности, подарочные карты)  | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| labels             | String | Marking codes list/Код маркировки (значеник кода DataMatrix). К примеру если   | 05367567230048c?eN1(o0029                   |
|                    |        | кол-во товаров с маркир. будет 5 шт, то в amount указываем 1 шт                |                                             |
| class_code         | Long   | Product class code/Код ИКПУ (МХИК) (tasnif.soliq.uz)                           | 10999001001000000                           |
| package_code       | Long   | Package_code/ Код ед.измерений / упаковки (tasnif.soliq.uz)                    | 1520627                                     |
| owner_type         | Integer| Owner_type/ Код происхождения товара (одно значение либо 0, либо 1, либо 2     | 0,1,2                                       |
|                    |        | (0-"Куплено и продано" / 1-"Собственное производство" / 2-"Поставщик услуг")   |                                             |
| comission_info     | Long   | Sign commission check TIN, PINFL/Признак комиссионный чек ИНН, ПИНФЛ           | 123456789, 12345678912345                   |
| uuid               | String | Your UUID / Ваш UUID                                                           | abc123                                      |
| time               | Double | Time in format yyyy-MM-dd hh:mm:ss/Дата и время в формате yyyy-MM-dd hh:mm:ss  | 2021-09-08 22:54:59                         |
| cashier            | String | Cashier name/Имя кассира                                                       | Админ                                       |
| received_cash      | Long   | Received cash price/Оплата наличными                                           | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| change             | Long   | Change price/Сдача                                                             | 100                                         |
| received_card      | Long   | Received cash price/Оплата банковской картой,Payme,Click,UZUM                  | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| card_type          | Integer| Card type(personal or corporate) / Тип карты (личная или корпоративная)        | 1,2                                         |
|                    |        | 2 - личная карта , 1 - корпоративная карта                                     |                                             |
| ppt_id             | Integer| Номер RRN (ppt_id) в слипе ответе от банквоского пинпада (Humo, Uzcard)        | 123456789012                                |
| scan2pay_paid      | Bool   | If the payment was made through the service Scan2Pay true or false             | true or false                               |
|                    |        | Если оплата была через сервис Scan2Pay true или false                          |                                             |
| scan2pay_id        | String | uuid from /payment/qr_pay/status / uuid из /payment/qr_pay/status              | 59bcc56b-1fcf-4752-9f5b-a3fffdf525ae        |
| open_cashbox       | String | Open cashbox device/Открытие денежнего ящика                                   | true = open, false = not open               |
| type               | String | Banner type - {text, barcode, qr_code}/Штрих-код, QR-код                       | barcode                                     |
| data               | String | Banner text/Рекламный текст                                                    | Скидка на следующую покупку 5%              |
| prices / name      | String | Price name/Наименование вида оплаты                                            | USD, VISA, MasterCard, Click, Payme, Uzum   |
| prices / price     | Long   | Price/Сумма                                                                    | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |
| prices / vat_type  | Long   | Vat type/Название налога и ставка                                              | НДС 15%                                     |
| prices / vat_price | Long   | Vat price/Сумма налога                                                         | 50 тийин = 50, 1 сум = 100, 100 сум = 10000 |



**Data example**

```json
{
  "number":1,
  "receipt_type":"order",
  "products":
  [
    {
     "name":"наименование товара или услуги",
     "barcode":"4780000000007", 
     "amount":1000,
     "unit_name":"litr",
     "price":50000,
     "product_price":50000, 
     "vat":6000, 
     "vat_percent":12,
     "discount":0,
     "discount_percent":0,
     "other":0,
     "labels":["05367567230048c?eN1(o0029"],
     "class_code":"02710001005000000",
     "package_code":1282556,
     "owner_type":1,  
     "comission_info":{
              "inn":"123456789",
              "pinfl":"12345678912345"
    }
    }
  ],
*"uuid":"123",
"time":"2021-04-07 12:52:02",
"cashier":"Admin", 
"received_cash":50000, 
"change":0, 
"received_card":0,
"card_type":2,
"ppt_id":"123456789012",
*"scan2pay_paid":true,
"extra_info":{
    *"phone_number":"998911234569",
    *"qr_payment_id":"123456789id12"
    *"qr_payment_provider":"0141"   
    *"scan2pay_id":"59bcc56b-1fcf-4752-9f5b-a3fffdf525ae"
      },
*"open_cashbox":true,
*"send_email":true,
*"email":"abdullo21113@gmail.com",
*"sms_phone_number" :"+998909999999",
*"banners":
[ 
  {
  "type":"text",
  "data": "Код скидки для следующий покупки"
  "style":{
                 "font_width":2,
                "font_height":100,
                "is_bold":true
            }
  },
  {
  "type":"barcode",
  "data":"23423423"
  "style":{
                 "font_width":2,
                "font_height":100,
                "is_bold":true
            },
  }
],
*"prices":
  [
    {
     "name":"PayMe", 
     "price":100000,
     "vat_type":"QQS", 
     "vat_price":200000
    }
  ], 
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
| receipt_count  | Integer| Receipt count/Номер чека                                            | 643                                                             |
| date_time      | Double | Date in format YYYYMMDDHHMMSS/Дата и время в формате ГГГГММДДЧЧММСС | 20200518221403                                                  |
| fiscal_sign    | Long   | Fiscal sign/Фискальный признак                                      | 248429044289                                                    |
| applet_version | Integer| Applet version/Версия аплета                                        | 0300                                                            |
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
   "unit_name":[unit name],
   "price":[product_price * amount],
   "product_price":[product_price multiplied to 100], 
   "vat":[nds price multiplied to 100], 
   "vat_percent":[nds percent],
   "discount":[discount price  multiplied to 100],
   "discount_percent":[discount price percent],
   "other":[other discount prices  multiplied to 100],
   "class_code":[product class code for marking],
  *"labels":[marking codes list],
   "package_code":[package_code],
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
    *"qr_payment_provider":"0141"
          },
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
     "amount":1000,
     "unit_name":"dona",
     "price":230000,
     "product_price":2300.0, 
     "vat":15000.0, 
     "vat_percent":12,
     "discount":115000.0,
     "discount_percent":50.0,
     "other":0.0,
     "labels":["05367567230048c?eN1(o0029"],
     "class_code":"04811001001000000",
     "package_code":1431970,
     "owner_type":1,
     "comission_info":{
              "inn":"123456789",
              "pinfl":"12345678912345"
    }
    }
  ],
*"uuid":"123",
"qr_code":"https://ofd.soliq.uz/check?t=UZ191211501001&r=1447&c=20220309125810&s=461313663448",
"time":"2021-04-15 14:35:02",
"cashier":"Admin", 
"received_cash":100000, 
"change":0,
"received_card":15000,
"card_type":2,
"ppt_id":"123456789012",
"extra_info":{
    *"phone_number":"998911234569",
    *"qr_payment_id":"123456789id12"
    *"qr_payment_provider":"0141"
          },
*"send_email":true,
*"email":"abdullo21113@gmail.com",
*"sms_phone_number" :"+998909999999",

*"prices":
  [
    {
     "name":"UPAY", 
     "price":100000,
     "vat_type":"TUZATISH QQS", 
     "vat_price":200000
    }
  ], 
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


