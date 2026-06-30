# INFO

Operation for get info / Получение информации 

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
  "version_code": [Version code],
  "is_updated": [Is updated],
  "cash_accomulator": [Cash accumulator],
  "card_accomulator": [Card accumulator],
  "vat_accomulator": [VAT accumulator],
  "borrowed_receipt_files_count": [Borrowed receipt files count],
  "f_report_current_index": [F-report current index],
  "first_unacknowledged_receipt_time": [First unacknowledged receipt time],
  "receipt_current_index": [Receipt current index],
  "receipts_allocated": [Receipts allocated],
  "receipts_capacity": [Receipts capacity],
  "z_report_current_index": [Z-report current index],
  "z_reports_allocated": [Z-reports allocated],
  "z_reports_capacity": [Z-reports capacity],
  },
  "error": {
    "code":[code of error],
    "message":[error message],
    "data":[extra data for error]
    },
  "is_success": [is success response] 
}
```

| Name                        | Type    | Description EN/RU                                                      | Example                                    |
| --------------------------- | ------- | ---------------------------------------------------------------------- | ------------------------------------------ |
| terminal_id                 | string  | Fiscal module number/Номер фискального модуля                          | UZ170703100189                             |
| applet_version              | string  | Fiscal module applet version/Версия аплета фискального модуля          | 0300                                       |
| current_receipt_seq         | string  | Current receipt seq/Порядковый номер чека                              | 836                                        |
| current_time                | string  | Current time/Дата и время                                              | 2021-09-08 19:29:59                        |
| last_operation_time         | string  | Last operation time/Дата и время последней операци                     | 2021-09-08 19:29:59                        |
| receipt_count               | integer | Receipt count/Количество не оправленных чеков                          | 1                                          |
| receipt_max_count           | integer | Receipt max count/Максимальное количетсов чеков в одной кассовой смене | 858                                        |
| zreport_count               | integer | Zreport count/Количекстов закрытых кассовых смен                       | 38                                         |
| zreport_max_count           | integer | Zreport max count/Максимальное количество закрытых кассовых смен         | 832                                        |
| available_persistent_memory | integer | Available persistent memory/Доступная постоянная память                | 32767                                      |
| available_reset_memory      | integer | Available reset memory/Доступная память для сброса                     | 8918                                       |
| available_deselect_memory   | integer | Available deselect memory/Доступная память для отмены выбора           | 8918                                       |
| cashbox_number              | string  | Cashbox number/Номер денежного ящика                                      | "1"                                        |
| version_code                | string  | Version code/Версия прошивки                                           | 1.12.1                                     |
| is_updated                  | boolean | Is updated/Обновление (false — no auto update, true — auto update)     | false                                      |
| cash_accomulator            | object or null | Cash accumulator/Накопитель наличных                              | {"Sale":1000,"Refund":0}                  |
| card_accomulator            | object or null | Card accumulator/Накопитель карты                                 | {"Sale":1000,"Refund":0}                  |
| vat_accomulator             | object or null | VAT accumulator/Накопитель НДС                                    | {"Sale":120,"Refund":0}                   |
| cash_accomulator.Sale       | integer | Cash sale amount/Сумма продаж наличными                                | 1000                                       |
| cash_accomulator.Refund     | integer | Cash refund amount/Сумма возврата наличными                            | 0                                          |
| card_accomulator.Sale       | integer | Card sale amount/Сумма продаж картой                                   | 1000                                       |
| card_accomulator.Refund     | integer | Card refund amount/Сумма возврата картой                               | 0                                          |
| vat_accomulator.Sale        | integer | VAT sale amount/Сумма НДС продаж                                       | 120                                        |
| vat_accomulator.Refund      | integer | VAT refund amount/Сумма НДС возврата                                   | 0                                          |
| borrowed_receipt_files_count | integer or null | Borrowed receipt files count/Количество заимствованных файлов чеков | 0                                          |
| f_report_current_index      | integer or null | F-report current index/Текущий индекс F-отчёта                    | 0                                          |
| first_unacknowledged_receipt_time | string or null | First unacknowledged receipt time/Время первого неподтверждённого чека | 2021-09-08 19:29:59                        |
| receipt_current_index       | integer or null | Receipt current index/Текущий индекс чека                         | 0                                          |
| receipts_allocated          | integer or null | Receipts allocated/Выделено чеков                                 | 0                                          |
| receipts_capacity           | integer or null | Receipts capacity/Ёмкость чеков                                   | 858                                        |
| z_report_current_index      | integer or null | Z-report current index/Текущий индекс Z-отчёта                    | 0                                          |
| z_reports_allocated         | integer or null | Z-reports allocated/Выделено Z-отчётов                            | 0                                          |
| z_reports_capacity          | integer or null | Z-reports capacity/Ёмкость Z-отчётов                              | 832                                        |
| error.code                  | integer | Error code/Код ошибки                                                  | 102                                        |
| error.message               | string  | Error message/Сообщение об ошибке                                        | FISCAL_MODULE_NOT_INITIALIZED              |
| error.data                  | string  | Extra error data/Дополнительные данные ошибки                            | null                                       |
| is_success                  | boolean | Success flag/Признак успешного ответа                                    | true                                       |

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
    "last_operation_time": "2021-09-08 19:32:39",
    "receipt_count": 0,
    "receipt_max_count": 858,
    "zreport_count": 38,
    "zreport_max_count": 832,
    "available_persistent_memory": 6100,
    "available_reset_memory": 1440,
    "available_deselect_memory": 1440,
    "cashbox_number": "1",
    "version_code": "1.12.1",
    "is_updated": false
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
