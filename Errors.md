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

# 📱EPS Errors

## UZUM FAST PAY ERRORS

| Код / Code                          | Сообщение / Message                                                                   | Описание (RU)                                                                                           | Description (EN)                                                                                                 |
|-------------------------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `apelsin.pay.authorization.error`   | Авторизация не прошла. Проверьте данные авторизации.                                  | Авторизация не прошла. Проверьте данные авторизации.                                                    | Authorization failed. Check the authorization data.                                                              |
| `apelsin.pay.safe.mode.on`          | Карта пользователя находится в безопасном режиме (Safe Mode).                         | Карта пользователя находится в безопасном режиме (Safe Mode).                                           | The user's card is in Safe Mode.                                                                                 |
| `apelsin.pay.service.not.working`   | Сервис временно недоступен.                                                           | Сервис временно недоступен.                                                                             | The service is temporarily unavailable.                                                                          |
| `apelsin.pay.wrong.prefix.otp.data` | Некорректный формат QR-кода: длина должна быть 43 символа, неверный префикс.          | Некорректный формат QR-кода: длина должна быть 43 символа, неверный префикс.                            | Invalid QR code format: the length must be 43 characters and the prefix is incorrect.                            |
| `apelsin.pay.unsupported.operation` | Операция не поддерживается системой.                                                  | Операция не поддерживается системой.                                                                    | The operation is not supported by the system.                                                                    |
| `apelsin.pay.reverse.not.allowed`   | Возврат средств для этого партнера недоступен.                                        | Возврат средств для этого партнера недоступен.                                                          | Refunds are not available for this partner.                                                                      |
| `unsupported.fiscal.url`            | Ссылка на фискализацию указана неверно.                                               | Ссылка на фискализацию указана неверно.                                                                 | The fiscalization URL is incorrect.                                                                              |
| `order.id.duplicated`               | Попытка повторной оплаты с тем же значением order_id.                                 | Попытка повторной оплаты с тем же значением order_id.                                                   | A repeated payment attempt was made with the same order_id value.                                                |
| `transaction.duplicated`            | Попытка повторной оплаты с тем же значением TransactionID.                            | Попытка повторной оплаты с тем же значением TransactionID.                                              | A repeated payment attempt was made with the same TransactionID value.                                           |
| `apelsin.pay.user.otp.data.expired` | Срок действия OTP-данных в QR-коде истек.                                             | Срок действия OTP-данных в QR-коде истек (возможно, некорректное время на устройстве клиента).          | The OTP data in the QR code has expired (possibly due to incorrect time on the client's device).                 |
| `device.not.registered`             | Устройство клиента не зарегистрировано в системе Uzum Bank.                           | Устройство клиента не зарегистрировано в системе Uzum Bank.                                             | The client's device is not registered in the Uzum Bank system.                                                   |
| `operation.not.found`               | Указанная операция не найдена, либо сервис не активен.                                | Указанная операция не найдена, либо сервис не активен.                                                  | The specified operation was not found, or the service is not active.                                             |
| `qr.duplicated`                     | Оплата по указанному QR-коду уже была проведена.                                      | Оплата по указанному QR-коду уже была проведена.                                                        | Payment using the specified QR code has already been completed.                                                  |
| `receipt.qr.only.yours`             | QR-код не распознан системой.                                                         | QR-код не распознан системой.                                                                           | The QR code was not recognized by the system.                                                                    |
| `user.card.not.found`               | Карта пользователя не найдена в системе.                                              | Карта пользователя не найдена в системе.                                                                | The user's card was not found in the system.                                                                     |
| `user.does.not.exist`               | Пользователь с указанными данными не найден.                                          | Пользователь с указанными данными не найден.                                                            | No user with the specified data was found.                                                                       |
| `external.service.unavailable`      | Внешний сервис, связанный с операцией, недоступен.                                    | Внешний сервис, связанный с операцией, недоступен.                                                      | The external service associated with the operation is unavailable.                                               |
| `limit.was.set`                     | Установлено ограничение на транзакцию со стороны Uzcard, Humo или другого провайдера. | Установлено ограничение на транзакцию со стороны Uzcard, Humo или другого провайдера.                   | A transaction limit has been imposed by Uzcard, Humo, or another provider.                                       |
| `operation.failed`                  | Операция не выполнена. Транзакция отклонена.                                          | Операция не выполнена. Транзакция отклонена.                                                            | The operation was not completed. The transaction was declined.                                                   |
| `operation.forbidden`               | Операция запрещена.                                                                   | Операция запрещена. Возможно, тип карты (Uzcard, Humo и др.) не поддерживается или сервис заблокирован. | The operation is forbidden. The card type (Uzcard, Humo, etc.) may be unsupported or the service may be blocked. |
| `operation.is.inProcess`            | Запрос обрабатывается.                                                                | Запрос обрабатывается. Ответ по транзакции от процессинга ещё не получен.                               | The request is being processed. A transaction response has not yet been received from the processing system.     |

## CLICK PASS ERRORS

| Код / Code | Сообщение / Message                                       | Описание (RU)                                                                                                                  | Description (EN)                                                                                               |
|------------|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| -301       | Ошибка сканирования. Попробуйте ещё раз.                  | Ошибка сканирования. Попробуйте ещё раз.                                                                                       | Scanning error. Please try again.                                                                              |
| -301       | Платеж ранее был принят                                   | Платеж ранее был принят.                                                                                                       | The payment was previously accepted.                                                                           |
| -301       | Неверный QR-код. Попробуйте ещё раз.                      | Неверный QR-код. Попробуйте ещё раз.                                                                                           | Invalid QR code. Please try again.                                                                             |
| -11        | Неверные данные поставщика                                | Неверные данные поставщика. В примечании к источнику указано: 11 и 12 возникают, когда указаны неверные ключи сервиса.         | Invalid provider data. The source notes that errors 11 and 12 occur when incorrect service keys are specified. |
| -12        | Неверные данные поставщика                                | Неверные данные поставщика. В примечании к источнику указано: 11 и 12 возникают, когда указаны неверные ключи сервиса.         | Invalid provider data. The source notes that errors 11 and 12 occur when incorrect service keys are specified. |
| -13        | Минимальная сумма оплаты {min limit}                      | Минимальная сумма оплаты {min limit}.                                                                                          | Minimum payment amount: {min limit}.                                                                           |
| -14        | Вы превысили максимальный лимит оплаты в день {max limit} | Превышена максимальная сумма оплаты. Максимальный дневной лимит: {max limit}.                                                  | The maximum payment amount has been exceeded. Maximum daily limit: {max limit}.                                |
| -15        | Неверная строка подписи данных.                           | Неверная строка подписи данных.                                                                                                | Invalid data signature string.                                                                                 |
| -19        | Клиент не найден                                          | Клиент не найден. В примечании к источнику указано, что ошибка возникает, если по QR-коду не удалось найти пользователя Click. | Client not found. The source notes that this error occurs when a Click user cannot be found by the QR code.    |

## PAYME GO ERRORS

| Код / Code | Сообщение / Message                                                                                                 | Описание (RU)                                                                                                       | Description (EN)                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| `-31001`   | Сервер "Paycom" недоступен. Попробуйте позже.                                                                       | Сервер "Paycom" недоступен. Попробуйте позже.                                                                       | The "Paycom" server is unavailable. Please try again later.                                                                   |
| `-31400`   | Карта не найдена.                                                                                                   | Карта не найдена.                                                                                                   | Card not found.                                                                                                               |
| `-31002`   | Сервер процессингового центра недоступен                                                                            | Сервер процессингового центра недоступен.                                                                           | The processing center server is unavailable.                                                                                  |
| `-31300`   | Неверный номер карты                                                                                                | Неверный номер карты.                                                                                               | Invalid card number.                                                                                                          |
| `-31630`   | Неверный номер карты                                                                                                | Неверный номер карты.                                                                                               | Invalid card number.                                                                                                          |
| `-31300`   | Карта с таким номером не найдена                                                                                    | Карта с таким номером не найдена.                                                                                   | No card with this number was found.                                                                                           |
| `-31300`   | Неверно указана дата истечения срока действия карты                                                                 | Неверно указана дата истечения срока действия карты.                                                                | The card expiration date is incorrect.                                                                                        |
| `-31001`   | Сервер "Paycom" недоступен. Попробуйте позже.                                                                       | Сервер "Paycom" недоступен. Попробуйте позже.                                                                       | The "Paycom" server is unavailable. Please try again later.                                                                   |
| `-31400`   | Устройство не найдено.                                                                                              | Устройство не найдено.                                                                                              | Device not found.                                                                                                             |
| `-31400`   | Устройство не синхронизировано.                                                                                     | Устройство не синхронизировано.                                                                                     | The device is not synchronized.                                                                                               |
| `-31400`   | Синхронизация устройства устарела.                                                                                  | Синхронизация устройства устарела.                                                                                  | The device synchronization is outdated.                                                                                       |
| `-31400`   | Временный код неверный.                                                                                             | Временный код неверный.                                                                                             | The temporary code is incorrect.                                                                                              |
| `-31602`   | Чек не найден или оплачен                                                                                           | Чек не найден или уже оплачен.                                                                                      | The receipt was not found or has already been paid.                                                                           |
| `-31601`   | Поставщик не найден или заблокирован                                                                                | Поставщик не найден или заблокирован.                                                                               | The provider was not found or is blocked.                                                                                     |
| `-31601`   | MerchantIsMaintenance                                                                                               | MerchantIsMaintenance.                                                                                              | MerchantIsMaintenance.                                                                                                        |
| `-31700`   | В связи с техническими работами в системе, временно приостановленны оплаты услуг.                                   | В связи с техническими работами в системе, временно приостановленны оплаты услуг.                                   | Service payments are temporarily suspended due to technical maintenance in the system.                                        |
| `-31101`   | Карта не обслуживается                                                                                              | Карта не обслуживается.                                                                                             | The card is not serviced.                                                                                                     |
| `-31620`   | Процессинговый центр недоступен                                                                                     | Процессинговый центр недоступен.                                                                                    | The processing center is unavailable.                                                                                         |
| `-31100`   | Процессинговый центр недоступен                                                                                     | Процессинговый центр недоступен.                                                                                    | The processing center is unavailable.                                                                                         |
| `-31624`   | Процессинговый центр недоступен                                                                                     | Процессинговый центр недоступен.                                                                                    | The processing center is unavailable.                                                                                         |
| `-31630`   | Неверная дата истечения карты                                                                                       | Неверная дата истечения карты.                                                                                      | Invalid card expiration date.                                                                                                 |
| `-31630`   | Оплата услуг данного поставщика картами не доступна.                                                                | Оплата услуг данного поставщика картами не доступна.                                                                | Card payments for this provider's services are unavailable.                                                                   |
| `-31630`   | Не включено смс уведомление                                                                                         | Не включено смс уведомление.                                                                                        | SMS notification is not enabled.                                                                                              |
| `-31630`   | Карта устарела                                                                                                      | Карта устарела.                                                                                                     | The card has expired / is outdated.                                                                                           |
| `-31630`   | Превышен лимит попыток ввода PIN-кода. Карта заблокирована.                                                         | Превышен лимит попыток ввода PIN-кода. Карта заблокирована.                                                         | The PIN entry attempt limit has been exceeded. The card is blocked.                                                           |
| `-31630`   | Карте доступны только PIN операции                                                                                  | Карте доступны только PIN операции.                                                                                 | Only PIN operations are available for the card.                                                                               |
| `-31630`   | Карта заблокирована.                                                                                                | Карта заблокирована.                                                                                                | The card is blocked.                                                                                                          |
| `-31630`   | Карта корпоративная. Прием платежей запрещен.                                                                       | Карта корпоративная. Прием платежей запрещен.                                                                       | The card is corporate. Payment acceptance is prohibited.                                                                      |
| `-31630`   | Недостаточно средств на карте                                                                                       | Недостаточно средств на карте.                                                                                      | Insufficient funds on the card.                                                                                               |
| `-31630`   | Перевод средств для корпоративных карт недоступен.                                                                  | Перевод средств для корпоративных карт недоступен.                                                                  | Money transfers are unavailable for corporate cards.                                                                          |
| `-31630`   | Данные получателя не должны совпадать с данными отправителя.                                                        | Данные получателя не должны совпадать с данными отправителя.                                                        | The recipient's details must not match the sender's details.                                                                  |
| `-31630`   | Карты данного банка недоступны для перевода средств                                                                 | Карты данного банка недоступны для перевода средств.                                                                | Cards from this bank are unavailable for money transfers.                                                                     |
| `-31630`   | Карта исчерпала лимит для отправки средств на текущий месяц                                                         | Карта исчерпала лимит для отправки средств на текущий месяц.                                                        | The card has exhausted its outgoing transfer limit for the current month.                                                     |
| `-31630`   | Сумма перевода больше чем остаток лимита для отправки средств на текущий месяц. Остаток лимита: &lt;######&gt; сум. | Сумма перевода больше чем остаток лимита для отправки средств на текущий месяц. Остаток лимита: &lt;######&gt; сум. | The transfer amount exceeds the remaining outgoing transfer limit for the current month. Remaining limit: &lt;######&gt; UZS. |
| `-31630`   | Валюта карты не позволяет оплатить данный чек.                                                                      | Валюта карты не позволяет оплатить данный чек.                                                                      | The card currency does not allow payment of this receipt.                                                                     |
| `-31623`   | Сервис поставщика услуг работает не корректно                                                                       | Сервис поставщика услуг работает не корректно.                                                                      | The service provider's service is not operating correctly.                                                                    |
| `-31900`   | Данный тип карты не обслуживается.                                                                                  | Данный тип карты не обслуживается.                                                                                  | This card type is not serviced.                                                                                               |
| `-31640`   | Ошибка при списания средств с карты.                                                                                | Ошибка при списания средств с карты.                                                                                | An error occurred while debiting funds from the card.                                                                         |
| `-31102`   | Данная операция не поддерживается                                                                                   | Данная операция не поддерживается.                                                                                  | This operation is not supported.                                                                                              |
| `-31901`   | Данный тип операции не поддерживается в процессинге.                                                                | Данный тип операции не поддерживается в процессинге.                                                                | This operation type is not supported by the processing system.                                                                |
