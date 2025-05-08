**ERROR_RECEIPT_INDEX_OUT_OF_BOUNDS** - номер чека неправильный / Check number is incorrect 

**ERROR_RECEIPT_MEMORY_FULL** - Память чека заполнена / The check memory is full

**ERROR_RECEIPT_TIME_PAST** - Исправить дату и время на кассе и повторить попытку. Дата и время регистрации чека или открытия/закрытия Z-отчета должна отличаться хотя бы на одну секунду от даты и времени последней операции / Correct the date and time on the cash register and try again. The date and time of receipt registration or opening/closing of the Z-report must differ from the date and time of the last transaction by at least one second

**ERROR_RECEIPT_STORE_DAYS_LIMIT_EXCEEDED** - Кол-во дней хранения чеков оффлайне превышено, следует отправить чеки командной /order/sendreceipt / Number of days to store receipts offline exceeded, receipts should be sent via command /order/sendreceipt

**ERROR_CLOSE_ZREPORT_TIME_PAST** - Время закрытие отчета старое / Report closing time is old

**ERROR_ZREPORT_SPACE_IS_FULL** - Память Z-отчета заполнена необходимо физическая замена фискального модуля / Z-report memory is full, physical replacement of the fiscal module is required 

**ERROR_ZREPORT_INDEX_OUT_OF_BOUNDS** - Номер Z-report не правильный / Z-report number is incorrect

**Fiscal drive locked** - Фискальный модуль заблокирован на стороне ОФД , возможно за неуплату / The fiscal module is blocked on the OFD side, possibly due to non-payment

**ERROR_CURRENT_ZREPORT_IS_EMPTY** - Текущий Z-report пустой , невозможно закрыть пустой Z отчет /  Current Z-report is empty, it is impossible to close empty Z-report

**ERROR_ZREPORT_IS_NOT_OPEN** - Z-report не открыт, нужно открыть смену / Z-report not opened, need to open

**ERROR_ZREPORT_OPEN_TIME_FORMAT_INVALID** - Формат времени открытия Z-report ошибочна / Z-report opening time format is incorrect

**ERROR_ZREPORT_IS_ALREADY_OPEN** - смена уже открыта , можно продолжать пробивать чеки / the shift is already open, you can continue punching checks

**ERROR_NOT_ENOUGH_CASH_FOR_REFUND** - Не достаточно средств для возврата (наличка) / Not enough funds for refund (cash)

**ERROR_NOT_ENOUGH_CARD_FOR_REFUND** - Не достаточно средств для возврата (пластик) / Not enough funds for return (plastic)

**ERROR_NOT_ENOUGH_VAT_FOR_REFUND** - Не достаточно средств для возврата (НДС) / Not enough funds for refund (VAT)

**ERROR_OPEN_ZREPORT_TIME_PAST** - Время открытия Z- report старое / Opening time Z- report old

**Invalid time, time should be before or equal to current time: 2023-12-07 13:22:54** - Время отправленное на FBOX с кассового ПО отличается ( + - 5 минут допустимо) / The time sent to FBOX from the cash register software differs (+ - 5 minutes is acceptable)

**Dobavьte IKPU(MXIK) kod v tovar/Mahsulotga MXIK kodini qo'shing** - Нет кода ИКПУ в товаре/услуге или имеется лишний пробел / There is no IKPU code in the product/service or there is an extra space

**Network error** - Нет интернета или нет связи с ОФД серверами для осуществления процедура возврата чека /  There is no internet or no connection with OFD servers to carry out the check return procedure

**You have invalid subscription, not multi user** - Сработала зашита от обращения с другого IP адреса. Нет подписки на услугу Multi User / Protection against access from another IP address has been triggered. No subscription to the Multi User service

**Subscription up to date** - Закончилась подписка за ЦТО / Subscription for KKM has expired

**U vas zadoljennost po abonentskoj plate, obratites' v CTO** - Закончилась подписка за ЦТО / Subscription for KKM has expired
