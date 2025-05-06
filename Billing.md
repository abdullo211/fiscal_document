# Authorization in billing

Authorization in billing / Авторизация в биллинг 

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

**Auth required** : YES

**Headers** : ```Autherization: Token <token_value>```

### 🇷🇺 Заголовок

| Заголовок     | Значение              | Описание                                                                 |
| ------------- | --------------------- | ------------------------------------------------------------------------ |
| Authorization | Token `<token_value>` | Токен авторизации. Указывается как `Token` и пробел перед самим токеном. |

### 🇬🇧 Header

| Header        | Value                 | Description                                                                               |
| ------------- | --------------------- | ----------------------------------------------------------------------------------------- |
| Authorization | Token `<token_value>` | Authorization token. Should be prefixed with `Token` and a space before the token itself. |


**Query** : 
```?start_date: YYYY-MM-DDTHH:MM:SS // pay attention to T between date and time```

```?end_date: YYYY-MM-DDTHH:MM:SS // pay attention to T between date and time```

```?inn: 123456789```

### 🇷🇺 Параметры запроса

| Параметр     | Тип    | Обязательный | Описание                                                                                                   |
| ------------ | ------ | ------------ | ---------------------------------------------------------------------------------------------------------- |
| `start_date` | String | Да           | Начальная дата в формате ISO 8601 (`YYYY-MM-DDTHH:MM:SS`). Обязательно наличие `T` между датой и временем. |
| `end_date`   | String | Да           | Конечная дата в формате ISO 8601 (`YYYY-MM-DDTHH:MM:SS`). Обязательно наличие `T` между датой и временем.  |
| `inn`        | String | Да           | ИНН (идентификационный номер налогоплательщика) компании, по которой осуществляется запрос.                |

### 🇬🇧 Query params

| Parameter     | Type   | Required | Description                                                                                             |
| ------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------- |
| `start_date`  | String | Yes      | Start date in ISO 8601 format (`YYYY-MM-DDTHH:MM:SS`). The presence of `T` between date and time is mandatory. |
| `end_date`    | String | Yes      | End date in ISO 8601 format (`YYYY-MM-DDTHH:MM:SS`). The presence of `T` between date and time is mandatory.   |
| `inn`         | String | Yes      | TIN (Tax Identification Number) of the company for which the request is made.                          |

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
