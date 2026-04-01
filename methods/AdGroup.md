# AdGroup

> Оригинал: [https://ads.vk.com/doc/api/resource/AdGroup](https://ads.vk.com/doc/api/resource/AdGroup)

---

## /api/v2/ad_groups/.json

Ресурс позволяющий получить/редактировать одну рекламную группу

### GET

Получение одной рекламной группы

Пример запроса

```HTTP

    GET /api/v2/ad_groups/6617841.json
```

Пример ответа

```HTTP

    {
        "id": 6617841,
        "name": "New ad group 2022-07-15 17:53",
        "package_id": 83
    }
```

Параметры

- fields - список полей в ответе

```HTTP

    /api/v2/ad_groups.json?fields=id,package_id
```

Доступные поля - описаны в [AdGroup](../object/AdGroup)

### POST

Редактирование рекламной группы

Пример запроса

```HTTP

    POST /api/v2/ad_groups/6617841.json
    {
        "name": "New name"
    }
```

Пример ответа

```HTTP

    HTTP 204
```

Возможные коды ответа

- 200/204 - группа сохранена
- 400 - ошибка валидации
- 404 - группа не найдена

Возможные коды ошибок

- invalid_package - пакет недоступен данному пользователю
- can_not_set - нельзя переключиться на указанный пакет
- step - неверный шаг при проставлении budget_limit. Изменение должно быть кратно значению budget_limit_step из АПИ `/api/v2/currencies.json` для валюты пользователя 
- not_allowed_for_package - изменения недоступны в этом пакете.
- pricelist_not_found - для pricelist_id не найдено ни одного прайслиста
- permission_required - недостаточно прав для изменения поля
- audit_pixel_invalid_roles - неправильные роли аудит-пикселя
- audit_pixel_max_count - превышен лимит на поличество аудит-пикселей
- audit_pixel_must_be_unique - аудит-пиксели должны быть уникальны
- audit_pixel_invalid_urls - у аудит-пикселя неправильный URL
- min_translation_hours - минимальное время трансляции в fulltime таргетинге должно быть не менее 8 часов
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
- recommended_not_available - стратегия `recommended` недоступна. Необходимо установить общий бюджет и период трансляции или ежедневный бюджет группы

### DELETE

Удаление рекламной группы

Пример запроса

```HTTP

    DELETE /api/v2/ad_groups/6617841.json
```

Пример ответа

```HTTP

    HTTP 204
```