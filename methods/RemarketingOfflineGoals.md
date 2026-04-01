# RemarketingOfflineGoals

> Оригинал: [https://ads.vk.com/doc/api/resource/RemarketingOfflineGoals](https://ads.vk.com/doc/api/resource/RemarketingOfflineGoals)

---

## /api/v2/remarketing/offline_goals.json

Ресурс, позволяющий создать новый или получить массив существующих списков оффлайн конверсий

Используется объект: [RemarketingOfflineGoal](../object/RemarketingOfflineGoal)

### GET

Получение массива списков оффлайн конверсий

Пример запроса

```HTTP

    GET /api/v2/remarketing/offline_goals.json
```

Пример ответа

```HTTP

    {
        "items": [
            {
                "id": 83213,
                "created": "2017-07-04 17:36:16",
                "updated": "2018-11-09 12:08:57",
                "name": "Список посещений магазина"
                "type": "phone"
                "attribution_period": 90,
                "load_status": "matched",
            },
            {
                ...
            }
        ]
    }

```

### POST

Создание списка оффлайн конверсий

Пример запроса

```HTTP

    POST /api/v2/remarketing/offline_goals.json

    Content-Type: multipart/form-data
    "list_users": Файл
    data = {
        "name": "Список посещений магазина",
        "attribution_period": 90,
        "type": "email"
    }
```

Возвращаемые коды статуса:

204 - Список оффлайн конверсий успешно добавлен.

400 - Ошибка валидации.8b:Tafe,