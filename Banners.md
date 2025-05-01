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
                "font_width": [ test for size with numbers ],
                "font_height": [ test for size with numbers ],
                "align": [ left , right or center ],
                "is_bold": [ true or false ]
            }
        },
         {
            "type": [ barcode ],
            "data": [ use only numbers ],
            "cut": [ true or false ],
            "style":{
                "font_width": [ test for size with numbers ],
                "font_height": [ test for size with numbers ],
                "align": [ left , right or center ]
                "is_bold": [ true or false ],
                "barcode_type":[ 10 ]
            }
        }
    ]
}
```

## **Content** :
```json
{
    "banners": [
        {
            "type": "text",
            "data": "МЕГА ТВИСТЕР:ХАШБРАУН ЛОМИТИК СЫРА 35000 ",
            "cut":false,
            "style":{
                "font_width":"20",
                "font_height":"1",
                "align":"left",
                "is_bold":false
            }
        },
         {
            "type": "barcode",
            "data": "6000",
            "cut":true,
            "style":{
                 "font_width":"5",
                "font_height":"70",
                "align":"left",
                "is_bold":false,
                "barcode_type":10
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

**Success example**
**Code** : `200 OK`
