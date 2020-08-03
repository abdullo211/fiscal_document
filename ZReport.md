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
