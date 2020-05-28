# INFO

Operation for get info

**URL** : `/info/`

**Method** : `GET`

**Auth required** : NO

## Response

```json
{
 "data":{
  "terminal_id": [terminal id], 
  "applet_version": [Applet version],
  "current_receipt_seq": [Current receipt sequence count],
  "current_time": [Current time],
  "receipt_count": [Receipt count],
  "receipt_max_count": [Max receipt count],
  "zreport_count": [Zreport count],
  "zreport_max_count": [ZReport max count],
  "available_persistent_memory": [Available persistent memory],
  "available_reset_memory": [Available reset memory],
  "available_deselect_memory": [Available deselect memory],
  "cashbox_number": [Cashbox number],
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
    "applet_version": "0300",
    "current_receipt_seq": "836",
    "current_time": "2020-05-28 22:27:15",
    "receipt_count": 0,
    "receipt_max_count": 858,
    "zreport_count": 38,
    "zreport_max_count": 832,
    "available_persistent_memory": 6100,
    "available_reset_memory": 1440,
    "available_deselect_memory": 1440,
    "cashbox_number": 2
  },
  "error": null,
  "is_success": true
}
```
**Error example**
**Condition** : If 'Fiscal module not initialized'
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
