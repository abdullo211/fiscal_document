## 🏦 Печать копии последней сверки итогов и транзакции проведенные через банковский пинпад (терминал) / Print a copy of the last reconciliation of totals and transactions carried out through a bank pinpad (terminal)
| Метод | URL                               | Описание (RU)                          | Description (EN)               |
| ----- | --------------------------------- | -------------------------------------- | ------------------------------ |
| `GET` | `payment/xumo_close/print_last`   | Печать последней закрытой смены Xumo   | Print last closed Xumo shift   |
| `GET` | `payment/uzcard_close/print_last` | Печать последней закрытой смены Uzcard | Print last closed Uzcard shift |
| `GET` | `payment/xumo/print_last`         | Печать последней транзакции Xumo       | Print last Xumo transaction    |
| `GET` | `payment/uzcard/print_last`       | Печать последней транзакции Uzcard     | Print last Uzcard transaction  |

## 🧾 Выборочная печать закрытых Z-отчетов / Selective Printing of Closed Z-Reports
| Метод | URL                                                      | Описание (RU)                                                                                                                                              | Description (EN)                                                                                                                                                                  |
| ----- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `GET` | `https://fbox.ngrok.io/zreport/info?number=1&print=true` | Печать уже закрытого Z-отчета по номеру.<br>`number=1` — последний отчет, `2` — предпоследний и т.д.<br>`print=true` — указывает системе напечатать отчет. | Print a previously closed Z-report by reverse order number.<br>`number=1` — most recent report, `2` — second most recent, etc.<br>`print=true` — triggers printing of the report. |
