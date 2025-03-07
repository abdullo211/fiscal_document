# Humo / Универсальная отмена (в рамках 1 смены) через пинпад (Ingenico iPP 320, Lane 3000, Lane 7000) Humo

Operation for create paymen via Humo PinPad

**URL** : `/payment/xumo`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "request_id": [Request ID / Номер чека с банковского слипа],
  "amount": [Payment price],
  "is_return": [true]
}
```
**Content** :
```json
{
  "request_id":650,
  "amount": 30000 (цена в сотых 00)
  "is_return":"true"
}
```

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
    "data": {
        "message": "
            ОБЫЧНЫЙ ТОВАР
         IP OOO JETI ASPAN
      TOSHKENT, BUNYODKOR 9 UY
ID Терм.:34112204      Номер смены 1
ID Орг.:011760574070401       Чек 14
          Отмена (CANCEL)
              ОДОБРЕНО
         ОПЕРАЦИЯ ОТМЕНЕНА
СУММА:                    300.00 UZS
AID:A0860001000001   HUMO- Cless EMV
Карта:HUMO
        986018******9831:01
Код авториз.:731333   Код ответа:400
RRN(ссылка) :416311639412
Дата:11/06/24 17:39:54
Univ. EMV POS 1.0.0/(MP) /681
                ***
@humocardbot-информация по вашей
карте
====================================

	"ppt_id": "416311639412"
    },
    "error": null,
    "is_success": true
}
```

# UzCard / Возврат через пинпад PAX A35 UzCard

Operation for create paymen via PAX A35 UzCard

**URL** : `/payment/uzcard`

**Method** : `POST`

**Auth required** : NO
## Request 
```json
{
  "request_id": [Request RRN / Номер RRN с банковского слипа],
  "amount": [Payment price],
  "is_return": [true]
}
```
**Content** :
```json
{
  "request_id":010965270742,
  "amount": 30000 (цена в сотых 00)
  "is_return":"true"
}
```

**Success example**
**Code** : `200 OK`

**Content** :
```json
{
    "data": {
        "message": "
            OOO TEST TIME
        Tashkent, Main str
       БЕСКОНТАКТНАЯ ОПЕРАЦИЯ
Номер операции:                  168
Терминал:                   00000013
Торговец:            000000900227899
Версия ПО:        SKappay v1.7.0_rc2
SN:                       2290268839
RRN                     010968002727
Дата             2025-03-07 14:54:27
Карта               544081******5040
Тип:               UZCARD-MASTERCARD
 
 
              Возврат
             500.00 UZS
              Одобрено
          Код ответа:000 
, pptId=010968002727), error=null, isSuccess=true
}
```
