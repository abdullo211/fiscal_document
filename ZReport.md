# ZREPORT

## Open ZReport
Operation for open ZReport

**URL** : `/zreport/open/`

**Method** : `GET`

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
Operation for close ZReport

**URL** : `/zreport/close/`

**Method** : `GET`

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

## Close ZReport with print
Operation for close ZReport

**URL** : `/zreport/close/`

**Method** : `POST`

**Auth required** : NO

## Request
```json
{
"close_zreport": [Close zreport true or false]
 "name": [zreport name], 
 "prices":[
  {
    "type":[Price type {UZS,USD,HUMO}]
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
   "type":"UZS",
   "price":240000
   }
 ]
}```


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
