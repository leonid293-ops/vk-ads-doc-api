# OrdPartnerSubAgent

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdPartnerSubAgent](https://ads.vk.com/doc/api/resource/OrdPartnerSubAgent)

---

## /api/v1/ord/partner/subagents/.json

Ресурс, позволяющий читать/редактировать  контрагента.

#### Описание полей:
##### `user_type` - может принимать следующие значения:
```
"physical" | "juridical" | "ip" | "foreign_physical" | "foreign_juridical" 
```

##### `role` - может принимать следующие значения:
```
[ "publisher"] | [ "ors"] | [ "publisher, ors"]
```

### GET

#### Запрос возвращает данные указанного контрагента.

##### Пример запроса:

```HTTP

   GET /api/v1/ord/partner/subagents/42.json
```

##### Пример ответа:

```HTTP
{
    "id": 42,
    "inn": "210987654321",
    "name": "Иван Иванов",
    "phone": "+79876543210",
    "role": [
        "ors"
    ],
    "site": "http://example2.com",
    "user_type": "physical"
    "foreign_epayment_method": null
    "foreign_oksm_country_code": null,
    "foreign_registration_number": null
}

```

### POST
#### Запрос изменяет данные указанного контрагента.

##### Пример запроса:

```HTTP
   POST /api/v1/ord/partner/subagents/42.json

{
    "user_type": "juridical",
    "role": [
        "publisher"
    ],
    "name": "Имя в кириллице для-юрика",
    "inn": "7743001840"
}
```
##### Пример ответа:
```HTTP
{
    "id": 42,
    "inn": "7743001840",
    "name": "Имя в кириллице для-юрика",
    "phone": "+79876543210",
    "role": [
        "publisher"
    ],
    "site": "http://example2.com",
    "user_type": "juridical"
    "foreign_epayment_method": null
    "foreign_oksm_country_code": null,
    "foreign_registration_number": null
}
```

#### Возвращаемые коды статуса:

##### 204 - Данные успешно изменены.
##### 400 - Ошибка валидации.

#### Примеры ошибок: 

1) Ошибки в формате данных (пустое значение, больше/меньше допустимого значения и т.д.):

```HTTP

    {
        "error": {
            "fields": {
                "description": {
                    "message": "Empty value",
                    "code": "required"
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```

```HTTP

    {
        "error": {
            "fields": {
                "status": {
                    "message": "Unallowed value",
                    "code": "unallowed_value",
                    "allowed_values": ["active", "deleted", "blocked"]
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```

2) Переданы не все необходимые поля И(ИЛИ) заполнены лишние для заданного user_type:
```HTTP
    {
        "error": {
            "message": "Validation failed",
            "code": "validation_failed",
            "fields": {
                "foreign_oksm_country_code": {
                    "code":"estricted with given conditions",
                    "message":"Can only be passed for foreign_juridical and foreign_physical"
                }
            }
        }
    }
```