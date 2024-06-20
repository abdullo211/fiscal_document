# Humo / Универсальная отмена через пинпад (Ingenico iPP 320, Lane 3000, Lane 7000) Humo

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
