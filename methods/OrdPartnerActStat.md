# OrdPartnerActStat

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdPartnerActStat](https://ads.vk.com/doc/api/resource/OrdPartnerActStat)

---

## /api/v1/ord/partner/acts/.json

Ресурс, для 
получения цепочки актов для всех площадок владельца кабинета за указанный период.

#### Описание полей:
##### *month* - всегда должен указываться в формате `YYYY-MM-01 (2024-01-01, 2023-11-01 и т.д.)`

### GET

#### Запрос cписок актов за указанный месяц.

##### Пример запроса:

```HTTP
   GET /api/v1/ord/partner/acts/2024-07-01.json
```

##### Пример ответа:

```HTTP
{
  "count": 5,
  "items": [
    {
      "id": 1,
      "url": "https://mail.ru",
      "name": "Мейл.РУ",
      "contracts_count": 3,
      "acts_count": 3,
      "total_amount": "100.123"
    },
    {
      "id": 2,
      "url": "https://vk.com",
      "name": "ВКонтакте",
      "contracts_count": 0,
      "acts_count": 0,
      "total_amount": "500.321"
    }
  ]
}
```

#### Возвращаемые коды статуса:

##### 200 - Данные успешно изменены.
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
```58:Teaa,