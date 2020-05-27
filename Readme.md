# Order

Operations for order

**URL** : `/order/create/`

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
   "amount":[product amount ],
   "price":[product_price * amount],
   "product_price":[product price], 
   "vat":[nds price], 
   "vat_percent":[nds percent ],
   "discount":[discount price],
   "discount_percent":[discount price percent],
   "other":[other discount prices] 
   }
], 
"time":[Time in format yyyy-MM-dd HH:mm:ss or null],
"cashier":[Cashier name], 
"received_cash":[received cash price], 
"change":[change price], 
"received_card":[received card price]
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
     "other":0.0 
    }
  ], 
"time":null,
"cashier":"Admin", 
"received_cash":100000, 
"change":0, 
"received_card":15000
}
 
}
```

## Response

```json
 {
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
  "TerminalID": "UZ170703100189", 
  "ReceiptSeq": 643,
  "DateTime": "20200518221403",
  "FiscalSign": "248429044289", "AppletVersion": "0300", "QRCodeURL":
  "https://ofd.soliq.uz/check?t=UZ170703100189&r=643&c=20200518221403&s=248429044289" 
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
    "code":101,
    "message":"Printer not working",
    "data":null
    },
"is_success": false 
}
```
