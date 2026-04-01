# AdPlan

> Оригинал: [https://ads.vk.com/doc/api/resource/AdPlan](https://ads.vk.com/doc/api/resource/AdPlan)

---

## /api/v2/ad_plans/(?Pd+).json

Ресурс позволяющий получить/редактировать одну рекламную кампанию

Используется объект: [AdPlan](../object/AdPlan)

### GET

Получение одной рекламной кампании

Пример запроса

```HTTP

    GET /api/v2/ad_plans/6617841.json
```

Пример ответа

```HTTP

    {
        "id": 6617841,
        "name": "New campaign 2016-07-15 17:53"
    }
```

Параметры

- fields - список полей в ответе

```HTTP

    /api/v2/ad_plans.json?fields=id,package_id
```

Доступные поля - описаны в [AdGroup](../object/AdGroup)

### POST

Редактирование рекламной кампании

Пример запроса

```HTTP

    POST /api/v2/ad_plans/6617841.json
    {
        "name": "New name"
    }
```

Пример ответа

```HTTP

    HTTP 204
```

Возможные коды ответа

- 200/204 - кампания сохранена
- 400 - ошибка валидации
- 404 - кампания не найдена

Возможные коды ошибок
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
- unallowed_field - поле недоступноae:T1364,