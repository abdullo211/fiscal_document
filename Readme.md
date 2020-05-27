# Login

Used to create order

**URL** : `/api/login/`

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

## Success Response

**Code** : `200 OK`

**Content example**

```json
{
    "token": "93144b288eb1fdccbe46d6fc0f241a51766ecd3d"
}
```

## Error Response

**Condition** : If 'username' and 'password' combination is wrong.

**Code** : `400 BAD REQUEST`

**Content** :

```json
{
    "non_field_errors": [
        "Unable to login with provided credentials."
    ]
}
```
