# Print NON fiscal documents via banners / Печать НЕ ФИСКАЛЬНЫХ чеков через баннер

**URL** : `/print/banner`

**Method** : `POST`

**Auth required** : NO

## Request 

```json
{
    "banners": [
        {
            "type": [ text ],
            "data": [ use text and numbers ],
            "cut": [ true or false ],
            "style":{
                "font_width": [ font size number ],
                "font_height": [ font size number ],
                "align": [ left , right or center ],
                "is_bold": [ true or false ],
                "qr_size": [ QR size number ]
            }
        },
         {
            "type": [ barcode ],
            "data": [ use only numbers ],
            "cut": [ true or false ],
            "style":{
                "font_width": [ font size number ],
                "font_height": [ font size number ],
                "align": [ left , right or center ],
                "is_bold": [ true or false ],
                "barcode_type":[ 10 ],
                "qr_size": [ QR size number ]
            }
        },
        {
            "type": [ qr_code or qr_code_frame ],
            "data": [ QR text ],
            "cut": [ true or false ],
            "style":{
                "qr_size": [ QR size number ],
                "align": [ left , right or center ]
            }
        }
    ]
}
```

| Field | Type | Required | Description EN/RU | Example |
| ----- | ---- | -------- | ----------------- | ------- |
| banners | array | Yes | List of banner objects/Список баннеров | |
| banners[].type | string | Yes | Banner type: `text`, `barcode`, `qr_code`, `qr_code_frame`/Тип баннера | text |
| banners[].data | string | Yes | Banner text or barcode data/Текст или данные штрих-кода | МЕГА ТВИСТЕР |
| banners[].cut | boolean | No | Cut paper after banner/Отрезать бумагу после баннера | false |
| banners[].style.font_width | integer | No | Font width/Ширина шрифта | 20 |
| banners[].style.font_height | integer | No | Font height/Высота шрифта | 1 |
| banners[].style.align | string | No | Alignment: `left`, `right`, `center`/Выравнивание | left |
| banners[].style.is_bold | boolean | No | Bold text/Жирный шрифт | false |
| banners[].style.barcode_type | integer | No | Barcode type (for `barcode` only)/Тип штрих-кода | 10 |
| banners[].style.qr_size | integer | No | QR code size (for `qr_code` and `qr_code_frame`)/Размер QR-кода | 5 |

## **Content** :
```json
{
    "banners": [
        {
            "type": "text",
            "data": "МЕГА ТВИСТЕР:ХАШБРАУН ЛОМИТИК СЫРА 35000 ",
            "cut": false,
            "style":{
                "font_width": 20,
                "font_height": 1,
                "align": "left",
                "is_bold": false,
                "qr_size": 5
            }
        },
         {
            "type": "barcode",
            "data": "6000",
            "cut": true,
            "style":{
                 "font_width": 5,
                "font_height": 70,
                "align": "left",
                "is_bold": false,
                "barcode_type": 10,
                "qr_size": 5
            }
        },
        {
            "type": "qr_code",
            "data": "https://example.com",
            "cut": true,
            "style":{
                "qr_size": 5,
                "align": "center"
            }
        }
    ]
}
```

## Response

```json
{
    "data": null,
    "error": null,
    "is_success": true
}
```

| Field | Type | Description EN/RU |
| ----- | ---- | ----------------- |
| data | null | Response data/Данные ответа |
| error | object or null | Error object/Объект ошибки |
| is_success | boolean | Success flag/Признак успешного ответа |

**Success example**
**Code** : `200 OK`
