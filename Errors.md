# 📋 Ошибки фискального модуля / Fiscal Module Errors

| Код ошибки / Error Code | Описание (RU) | Description (EN) |
|-------------------------|----------------|------------------|
| `ERROR_RECEIPT_INDEX_OUT_OF_BOUNDS` | Номер чека неправильный | Check number is incorrect |
| `ERROR_RECEIPT_MEMORY_FULL` | Память чека заполнена | The check memory is full |
| `ERROR_RECEIPT_TIME_PAST` | Исправить дату и время на кассе и повторить попытку. Время операции должно отличаться минимум на 1 секунду от последней. | Correct the date and time on the cash register. Time must differ by at least 1 second from the last transaction. |
| `ERROR_RECEIPT_STORE_DAYS_LIMIT_EXCEEDED` | Превышено количество дней хранения чеков в оффлайне. Отправьте чеки через `/order/sendreceipt`. | Number of days to store receipts offline exceeded. Send via `/order/sendreceipt`. |
| `ERROR_CLOSE_ZREPORT_TIME_PAST` | Время закрытия Z-отчета устарело | Report closing time is old |
| `ERROR_ZREPORT_SPACE_IS_FULL` | Память Z-отчетов заполнена. Требуется замена фискального модуля | Z-report memory is full. Physical replacement of the fiscal module is required |
| `ERROR_ZREPORT_INDEX_OUT_OF_BOUNDS` | Неверный номер Z-отчета | Z-report number is incorrect |
| `Fiscal drive locked` | Фискальный модуль заблокирован (возможно за неуплату) | The fiscal module is blocked (possibly due to non-payment) |
| `ERROR_CURRENT_ZREPORT_IS_EMPTY` | Текущий Z-отчет пустой. Нельзя закрыть пустой Z-отчет | Current Z-report is empty. Cannot close an empty report |
| `ERROR_ZREPORT_IS_NOT_OPEN` | Z-отчет не открыт. Нужно открыть смену | Z-report not opened. Need to open shift |
| `ERROR_ZREPORT_OPEN_TIME_FORMAT_INVALID` | Неверный формат времени открытия Z-отчета | Z-report opening time format is incorrect |
| `ERROR_ZREPORT_IS_ALREADY_OPEN` | Смена уже открыта. Можно продолжать работу | Shift is already open. You can continue punching checks |
| `ERROR_NOT_ENOUGH_CASH_FOR_REFUND` | Недостаточно наличных для возврата | Not enough cash for refund |
| `ERROR_NOT_ENOUGH_CARD_FOR_REFUND` | Недостаточно средств на карте для возврата | Not enough card funds for refund |
| `ERROR_NOT_ENOUGH_VAT_FOR_REFUND` | Недостаточно средств (НДС) для возврата | Not enough VAT funds for refund |
| `ERROR_OPEN_ZREPORT_TIME_PAST` | Время открытия Z-отчета устарело | Opening time of Z-report is old |
| `Network error` | Нет интернета или связи с ОФД для возврата чека | No internet or connection with OFD for check return |

## 🧾 Ошибки FiscalBox / FiscalBox Errors

| Сообщение / Message | Описание (RU) | Description (EN) |
|---------------------|----------------|------------------|
| `Invalid time...` | Время отличается более чем на ±5 минут от текущего | Time differs more than ±5 minutes from current |
| `Dobavьte IKPU(MXIK)...` | Нет кода ИКПУ или есть лишний пробел | No IKPU code or extra space in product |
| `You have invalid subscription...` | Доступ с другого IP. Нет подписки Multi User | Access from another IP. No Multi User subscription |
| `Subscription up to date` | Подписка ЦТО истекла | CTO subscription expired |
| `U vas zadoljennost...` | Подписка ЦТО истекла | CTO subscription expired |

## ⚠️ Прочие коды ошибок / Other Error Codes

| Код / Code | Описание | Description |
|------------|----------|-------------|
| `PRINTER_NOT_WORKING (101)` | Принтер не работает | Printer not working |
| `SAVE_ORDER_ERROR (303)` | Ошибка сохранения заказа | Order save error |
| `INTERNAL_ERROR (103)` | Внутренняя ошибка | Internal error |
| `INVALID_ARGUMENT (104)` | Неверный аргумент | Invalid argument |
| `SUBSCRIPTION_UP_TO_DATE (333)` | Подписка ЦТО истекла | CTO subscription expired |
| `INVALID_SUBSCRIPTION_MULTI__USER (444)` | Нет подписки Multi User | No Multi User subscription |
| `INVALID_CLASS_CODE (401)` | Неверный ИКПУ код | Invalid IKPU code |
| `SCAN2PAY_TRANSACTION_NOT_FOUND (403)` | Транзакция по Scan2Pay не найдена | Scan2Pay transaction not found |
| `BILLING_ERROR (105)` | Ошибка биллинга | Billing error |
| `XUMO_ERROR (108)` | Ошибка XUMO | XUMO error |
| `UZKARD_ERROR (109)` | Ошибка Uzcard | Uzcard error |
| `PAYMENT_ERROR (106)` | Ошибка оплаты | Payment error |
