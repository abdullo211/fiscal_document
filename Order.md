# ORDER

## Order create
Operation for create order

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
   "name":[product name String], 
   "barcode":[product barcode String], 
   "amount":[product amount  multiplied by 1000],
   "price":[product_price * amount],
   "product_price":[product_price multiplied by 100], 
   "vat":[nds price multiplied by 100], 
   "vat_percent":[nds percent],
   "discount":[discount price  multiplied by 100],
   "discount_percent":[discount price percent],
   "other":[other discount prices  multiplied by 100],
  *"labels":[marking codes list],
  *"class_code":[product class code for marking]
   }
], 
"time":[Time in format yyyy-MM-dd HH:mm:ss],
"cashier":[Cashier name], 
"received_cash":[received cash price  multiplied by 100], 
"change":[change price multiplied by 100], 
"received_card":[received card price  multiplied by 100],
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
   "name":[price name String], 
   "price":[price multiplied by 100], 
   "vat_type":[vat name String],
   "vat_price":[vat price multiplied by 100],
   }
] 
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
"time":"2021-04-07 12:52:02",
"cashier":"Admin", 
"received_cash":100000, 
"change":0, 
"received_card":15000,
"open_cashbox":true,
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
Operations for refuse order

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
Operation for print last order 

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


