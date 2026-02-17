# 📋 Ошибки фискального модуля / Fiscal Module Errors

| Код / Code | Код ошибки / Error Code | Описание (RU) | Description (EN) |
|----|-------------------------|----------------|------------------|
| `36871` | `ERROR_RECEIPT_INDEX_OUT_OF_BOUNDS` | Номер чека неправильный | Check number is incorrect |
| `36886` | `ERROR_RECEIPT_MEMORY_FULL` | Память чека заполнена | The check memory is full |
| `36888` | `ERROR_RECEIPT_TIME_PAST` | Исправить дату и время на кассе и повторить попытку. Время операции должно отличаться минимум на 1 секунду от последней. | Correct the date and time on the cash register. Time must differ by at least 1 second from the last transaction. |
| `36889` | `ERROR_RECEIPT_STORE_DAYS_LIMIT_EXCEEDED` | Превышено количество дней хранения чеков в оффлайне. Отправьте чеки через `/order/sendreceipt`. | Number of days to store receipts offline exceeded. Send via `/order/sendreceipt`. |
| `36897` | `ERROR_CLOSE_ZREPORT_TIME_PAST` | Время закрытия Z-отчета устарело | Report closing time is old |
| `36898` | `ERROR_ZREPORT_SPACE_IS_FULL` | Память Z-отчетов заполнена. Требуется замена фискального модуля | Z-report memory is full. Physical replacement of the fiscal module is required |
| `36902` | `ERROR_ZREPORT_INDEX_OUT_OF_BOUNDS` | Неверный номер Z-отчета | Z-report number is incorrect |
| `65279` | `Fiscal drive locked` | Фискальный модуль заблокирован (возможно за неуплату) | The fiscal module is blocked (possibly due to non-payment) |
| `36907` | `ERROR_CURRENT_ZREPORT_IS_EMPTY` | Текущий Z-отчет пустой. Нельзя закрыть пустой Z-отчет | Current Z-report is empty. Cannot close an empty report |
| `36909` | `ERROR_ZREPORT_IS_NOT_OPEN` | Z-отчет не открыт. Нужно открыть смену | Z-report not opened. Need to open shift |
| `36910` | `ERROR_ZREPORT_OPEN_TIME_FORMAT_INVALID` | Неверный формат времени открытия Z-отчета | Z-report opening time format is incorrect |
| `36912` | `ERROR_ZREPORT_IS_ALREADY_OPEN` | Смена уже открыта. Можно продолжать работу | Shift is already open. You can continue punching checks |
| `36913` | `ERROR_NOT_ENOUGH_CASH_FOR_REFUND` | Недостаточно наличных для возврата | Not enough cash for refund |
| `36914` | `ERROR_NOT_ENOUGH_CARD_FOR_REFUND` | Недостаточно средств на карте для возврата | Not enough card funds for refund |
| `36915` | `ERROR_NOT_ENOUGH_VAT_FOR_REFUND` | Недостаточно средств (НДС) для возврата | Not enough VAT funds for refund |
| `36916` | `ERROR_OPEN_ZREPORT_TIME_PAST` | Время открытия Z-отчета устарело | Opening time of Z-report is old |
| `65274` | `not valid refund info` | При регистрации чека возврата была передана информация об отозванном чеке (RefundInfo) с недействительным ФП | When registering a refund check, information about a revoked check (RefundInfo) with an invalid FP was transmitted |
| `65276` | `bad refund info passed` | При регистрации чека возврата была передана информация об отозванном чеке (RefundInfo) с неправильными значениями | When registering a refund check, the refunded check information (RefundInfo) was transmitted with incorrect values |
| `65277` | `no refund info passed` | При регистрации чека возврата не была передана информация об отозванном чеке (qr_code) | When registering a refund check, information about the revoked check (qr_code) was not transmitted |
| `65531` | `cannot encode receipt` | В переданном чеке есть ошибочные параметры, не соблюдаются условия уравнения , суммы товаров , суммы чека | The submitted check contains erroneous parameters, the conditions of the equation, the amount of goods, and the amount of the check are not met |
| `65532` | `illegal argument` | Передан недействительный параметр в JSON | An invalid parameter was passed in JSON |
| `65534` | `cannot connect card` | Не удалось подключится к ФМ, ФМ не подключен | Failed to connect to FM, FM not connected |

## 🧾 Ошибки FiscalBox / FiscalBox Errors

| Код / Code | Сообщение / Message | Описание (RU) | Description (EN) |
|------------|---------------------|----------------|------------------|
| `104` | `Invalid time...` | Время отличается более чем на ±5 минут от текущего | Time differs more than ±5 minutes from current |
| `401` | `Dobavьte IKPU(MXIK)...` | Нет кода ИКПУ или есть лишний пробел | No IKPU code or extra space in product |
| `444` | `You have invalid subscription...` | Доступ с другого IP. Нет подписки Multi User | Access from another IP. No Multi User subscription |
| `333` | `Subscription up to date` | Подписка ЦТО истекла | CTO subscription expired |
| `333` | `U vas zadoljennost...` | Подписка ЦТО истекла | CTO subscription expired |
| `402` | `Неправильный код упаковки для товара...` | Неверный код упаковки (единицы измерения) |  Invalid package code (units of measurement) |
| `402` | `Добавьте код маркировки для товара...` | Не добавлен код маркировки для товра | The mark code for the product has not been added |

## ⚠️ Прочие коды ошибок / Other Error Codes

| Код / Code | Описание | Description |
|------------|----------|-------------|
| `101` | Принтер не работает | PRINTER_NOT_WORKING |
| `303` | Ошибка сохранения заказа | SAVE_ORDER_ERROR |
| `103` | Внутренняя ошибка | INTERNAL_ERROR |
| `104` | Неверный аргумент | INVALID_ARGUMENT |
| `333` | Подписка ЦТО истекла | SUBSCRIPTION_UP_TO_DATE |
| `444` | Нет подписки Multi User |INVALID_SUBSCRIPTION_MULTI__USER |
| `401` | Неверный ИКПУ код | INVALID_CLASS_CODE, Invalid IKPU code |
| `403` | Транзакция по Scan2Pay не найдена | SCAN2PAY_TRANSACTION_NOT_FOUND |
| `105` | Ошибка биллинга | BILLING_ERROR |
| `108` | Ошибка XUMO | XUMO_ERROR |
| `109` | Ошибка Uzcard | UZKARD_ERROR |
| `106` | Ошибка оплаты | PAYMENT_ERROR |

## 🏦 Ошибки банковских пинпадов (терминалов) / Bank PIN Pad (Terminal) Errors

| Код / Code | Описание (RU) | Description (EN) |
|------------|---------------|------------------|
| `000` | Успешно | Successful |
| `001` | Успешно с МСС из списка 7995, 7511, 6051, 6010, 4829 | Successful with MCC from list |
| `003` | Успешная транзакция | Transaction successful |
| `005` | Системная ошибка | System error |
| `006` | Отказ ввода карты / операции | Card input or transaction declined |
| `020` | Успешно (отрицательный баланс) | Success (with negative balance) |
| `095` | Ошибка сверки итогов | Reconcile error |
| `100` | Транзакция не одобрена | Transaction not approved |
| `101` | Карта просрочена | Card expired |
| `103` | Необходим звонок эмитенту | Call issuer |
| `104` | Карта ограничена | Card restricted |
| `105` | Вызовите охрану | Call security |
| `106` | Многократная ошибка ПИН | Multiple PIN errors |
| `107` | Необходим звонок эмитенту | Call issuer |
| `109` | Неверный ID торговца | Invalid merchant ID |
| `110` | Невозможно обработать сумму | Cannot process amount |
| `111` | Неверный счет | Invalid account |
| `116` | Недостаточно средств | Insufficient funds |
| `117` | Неверный ПИН | Invalid PIN |
| `118` | Запрос отклонен банком | Bank declined |
| `119` | Транзакция противозаконна | Illegal transaction |
| `120` | Не разрешена | Not permitted |
| `121` | Превышен лимит наличных | Cash limit exceeded |
| `123` | Циклический лимит исчерпан | Cyclic limit exceeded |
| `125` | Плохая карта | Bad card |
| `126–128` | Ошибка обработки ПИН | PIN processing error |
| `200` | Испорченная карта | Damaged card |
| `201` | Необходим номер чека / карта просрочена | Receipt number needed / Card expired |
| `202` | Транзакция не найдена | Transaction not found |
| `203` | Отказ ввода суммы / вызовите охрану | Amount input declined / Call security |
| `204` | Счет заблокирован | Account blocked |
| `205` | Отказ ввода ссылки / вызовите охрану | Reference input declined / Call security |
| `206` | Отказ от подтверждения отмены | Cancellation not confirmed |
| `207` | Неверный код авторизации | Invalid auth code |
| `208` | Отказ ввода CVV2 | CVV2 input declined |
| `209` | Карта украдена | Stolen card |
| `210` | Следующего чека нет | No next receipt |
| `211` | Отказ ввода пин-кода | PIN entry declined |
| `212` | Отмена операции кассой | Operation cancelled by cashier |
| `213` | Отказ чтения карты коммерсанта | Merchant card read error |
| `214` | Неверный ручной ввод | Invalid manual input |
| `215` | Отказ ввода типа карты | Card type input declined |
| `216` | Отказ выбора операции | Operation selection declined |
| `217` | Отмена по чужой карте | Foreign card cancellation |
| `218` | Операция уже отменена | Operation already cancelled |
| `222` | Ошибка Track2 / Поиск транзакции | Track2 / transaction search error |
| `230` | Отказ ввода кода авторизации (Amex) | Amex auth code declined |
| `233` | Карта не прочитана | Card not read |
| `234` | Ошибка чтения чипа | Chip read error |
| `235` | Превышена сумма оригинальной операции | Original transaction amount exceeded |
| `240–243` | Ошибки TMS (ARCUS) | TMS (ARCUS) errors |
| `250` | Карта извлечена до окончания | Card removed too early |
| `301` | Не задан ID терминала | Terminal ID not set |
| `302` | Невозможно отменить операцию | Cannot cancel operation |
| `303` | Журнал переполнен | Journal overflow (close shift required) |
| `304` | Валюта не поддерживается | Currency not supported |
| `305` | Карта не обслуживается | Card not accepted |
| `320` | Отказ от подписи | Signature declined |
| `321` | Слишком большая сумма | Amount too large |
| `401` | Ошибка чтения карты мерчанта | Merchant card read error |
| `402–403` | Ошибка связи / конфигурации | Communication/config error |
| `404` | Неверный формат ответа | Invalid host response |
| `405` | Нет отложенных операций | No pending transactions |
| `410` | Ошибка загрузки ключей | Key load error |
| `411` | Таймаут чтения карты | Card read timeout |
| `902` | Неверная операция | Invalid operation |
| `903` | Повторите транзакцию | Retry transaction |
| `904` | Неверный формат сообщения | Invalid message format |
| `905–910` | Эмитент не работает / отказ | Issuer error / system failure |
| `911` | Неизвестная транзакция (SmartVista) | SmartVista doesn't know how to handle |
| `912` | Таймаут ответа | Timeout |
| `913` | Дубликат транзакции | Duplicate transaction |
| `914` | Оригинальная транзакция не найдена | Original transaction not found |
| `915` | Сумма отмены больше оригинала | Cancel amount > original |
| `916` | Долг не найден | Debt not found |
| `920` | Ошибка обработки ПИН | PIN processing error |
| `923` | Запрос обрабатывается | Request in progress |
| `940` | Заберите карту | Remove card |
| `941` | Не задан список операций | No operation list set |
| `984` | ПИН-ПАД занят | PIN pad busy |
| `985` | Ошибка MIFARE DIRECT | MIFARE direct error |
| `987` | Таймаут чтения карты | Card read timeout |
| `988` | Ошибка формата / память слипов переполнена | Format error / slip memory full |
| `989` | Ошибка Track2 | Track2 read error |
| `990` | Отказ ввода карты / проведения | Card/operation declined |
| `991` | Неверная Expiration Date | Invalid Expiry Date |
| `992` | Операция прервана клиентом/кассиром | Operation aborted |
| `996` | Неверный формат запроса | Invalid request format |
| `998` | Ошибка связи, позвоните в банк | Communication error, call bank |
| `999` | Нет связи с ПИН-ПАДом | No connection with PIN pad |

