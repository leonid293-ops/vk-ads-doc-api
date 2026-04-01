# AdPlans

> Оригинал: [https://ads.vk.com/doc/api/resource/AdPlans](https://ads.vk.com/doc/api/resource/AdPlans)

---

## /api/v2/ad_plans.json

Ресурс, позволяющий создать новую или получить список существующих рекламных кампаний

Используется объект: [AdPlan](../object/AdPlan)

### GET

Получение списка рекламных кампаний

Пример запроса

```HTTP

    GET /api/v2/ad_plans.json
```

Пример ответа

```HTTP

    {
        "count": 3,
        "offset": 0,
        "items": [
            {
                "id": 6617841,
                "name": "New campaign 2022-07-15 17:53"
            },
            {
                "id": 6711647,
                "name": "New campaign 2022-08-16 19:49"
            },
            {
                "id": 6711665,
                "name": "New campaign 2022-08-16 19:51"
            }
        ]
    }
```

Доступные поля - описаны в [AdPlan](../object/AdPlan)

Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

- limit - количество кампаний в ответе. По умолчанию 20

```HTTP

    /api/v2/ad_plans.json?limit=10
```

- offset - смещение на N кампаний от начала текущей выборки

```HTTP

    /api/v2/ad_plans.json?limit=5&offset=15
```

Фильтры

- _id - ID кампании

```HTTP

    /api/v2/ad_plans.json?_id=6617841
    /api/v2/ad_plans.json?_id__in=6617841,6711647
```

- _status - статус кампании. Доступные статусы "active", "blocked", "deleted"

```HTTP

    /api/v2/ad_plans.json?_status=active
    /api/v2/ad_plans.json?_status__ne=active
    /api/v2/ad_plans.json?_status__in=active,blocked
```

Сортировка

- id

```HTTP

    /api/v2/ad_plans.json?sorting=id - по возрастанию
    /api/v2/ad_plans.json?sorting=-id - по убыванию
```

- name

```HTTP

    /api/v2/ad_plans.json?sorting=name - по возрастанию
    /api/v2/ad_plans.json?sorting=-name - по убыванию
```

- status

```HTTP

    /api/v2/ad_plans.json?sorting=status - по возрастанию
    /api/v2/ad_plans.json?sorting=-status - по убыванию
```

- по нескольким полям

```HTTP

    /api/v2/ad_plans.json?sorting=status,name,-id

```

### POST

Создание рекламной кампании

Пример запроса:

```HTTP

    POST /api/v2/ad_plans.json
    {
        "name": "Моя новая кампания",
        "status": "active",
        "date_start": "2022-04-01 00:00:00",
        "date_end": "2022-04-15 00:00:00",
        "autobidding_mode": "max_goals",
        "budget_limit_day": "1000",
        "budget_limit": "5000",
        "enable_utm": "False",
        "enable_offline_goals": "False",
        "objective": "playersengagement",
        "ad_groups": []
    }
```

Пример ответа:

```HTTP

    HTTP 200
    {
        "id": 9826424
    }
```

В ответе всегда присутствуют поля id и ad_groups (если кампания создается с группами).
Важно! ad_groups неподдерживается в fields и возвращается ошибка.

Возможно создавать кампанию с одним из статусов: active, blocked, deleted.
Если статус не передан, то устанавливается статус active.

Возможные коды ответа

- 200/204 - кампания сохранена
- 400 - ошибка валидации

Возможные коды ошибок:
- pricelist_not_found - для pricelist_id не найдено ни одного прайслиста
- permission_required - недостаточно прав для изменения поля
- required - поле обязательно
- max_value - значение больше максимального
- min_value - значение меньше минимального
- bad_value - неправильный формат или тип значения
- bad_items - в списке присутствуют неправильные значения
- read_only_field - поле только для чтения
- duplicate_value - значения повторяются
- required_value - ожидаются обязательные значения
- required_one_of_value - ожидается одно из обязательных значении
- unallowed_value - значение не входит в список достимых
- unallowed_field - поле недоступно

В общем случае сообщение о ошибке имеет следующий формат:

```HTTP

    {
        "error": {
            "fields": {
                "": {
                    "message": "",
                    "code": ""
                },
                "": {
                    "message": "",
                    "code": ""
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```

где field_name_N - название поля, в котором произошла ошибка, error_message_N - описание ошибки, error_code_N - код ошибки.

Пример:

```HTTP

    {
        "error": {
            "fields": {
                "audit_pixels": {
                    "message": "Error validating audit pixels urls",
                    "code": "audit_pixel_invalid_urls"
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```