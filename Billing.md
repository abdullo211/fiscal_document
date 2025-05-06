# Enter to billing

Enter to billing / Вход в биллинг 

**URL** : `https://api.fbox.uz/api/v1/login/`

**Method** : `POST`

**Auth required** : NO

**Data constraints***
```json
{
    "username": [Login],
    "password": [Password]
}
```
## Response

```json
{
    "token": [Number and digit]
}
```

# Orders count

Operation for orders count / Получение информации о продажах 

**URL** : `https://api.fbox.uz/api/v1/orders/count/`

**Method** : `GET`

**Auth required** : NO

**Query** : 
```?start_date: YYYY-MM-DDTHH:MM:SS // pay attention to T between date and time```

```?end_date: YYYY-MM-DDTHH:MM:SS // pay attention to T between date and time```

```?inn: 123456789```

**Data constraints**
```json
{
    "status": [Status],
    "filters": {
        "start_date": [Start date],
        "end_date": [End date],
        "inn": [INN Company]
    },
    "data": {
        "total_orders": [Orders count],
        "total_amount": [Total sum]
    }
}
```

## Response
```json
{
    "status": "successfully",
    "filters": {
        "start_date": "2025-05-05T00:00:00",
        "end_date": "2025-05-05T23:59:59",
        "inn": "306429662"
    },
    "data": {
        "total_orders": 2,
        "total_amount": 700.0
    }
}
```
