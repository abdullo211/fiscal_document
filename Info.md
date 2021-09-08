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
  "last_operation_time":  [Last operation time],
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
| Name                              | Type          | Description EN/RU                                                            | Example                                  |
| --------------------------------- | ------------- | ---------------------------------------------------------------------------- | ---------------------------------------- |
| terminal_id                       | String        | Fiscal module number/Номер фискального модуля                                | UZ170703100189                           |
| applet_version                    | String        | Fiscal module applet version/Версия аплета фискального модуля                | 0300                                     |
| current_receipt_seq               | String        | Current receipt seq/Порядковый номер чека                                    | 836                                      |
| current_time                      | String        | Current time/Дата и время                                                    | 2021-09-08 19:29:59                      |
| last_operation_time               | String        | Last operation time/Дата и время последней операци                           | 2021-09-08 19:29:59                      |
| receipt_count                     | String        | Receipt count/Количество не оправленных чековы                               | 1                                        |
| receipt_max_count                 | String        | Receipt max count/Максимальное количетсов чеков в одной кассовой смене       | 858                                      |
| zreport_count                     | String        | Zreport count/Количекстов закрытых кассовых смен                             | 38                                       |
| zreport_max_count                 | String        | Zreport_max_count/Количекстов закрытых кассовых смен                         | 832                                      |
| available_persistent_memory       | String        | Available persistent memory/Доступная постоянная память                      | 32767                                    |
| available_reset_memory            | String        | Available reset memory/Доступная память для сброса                           | 8918                                     |
| available_deselect_memory         | String        | Available deselect memory/Доступная память для отмены выбора                 | 8918                                     |
| cashbox_number                    | String        | Cashbox number/Денежный ящик                                                 | 0 - no open, 1 - open                    |


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
    "last_operation_time": "2021-09-08 19:32:39"
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
