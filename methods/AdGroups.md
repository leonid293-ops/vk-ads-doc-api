# AdGroups

> Оригинал: [https://ads.vk.com/doc/api/resource/AdGroups](https://ads.vk.com/doc/api/resource/AdGroups)

---

## /api/v2/ad_groups.json

Ресурс, позволяющий создать новую или получить список существующих рекламных групп

Используется объект: [AdGroup](../object/AdGroup)

### GET

Получение списка рекламных групп

Пример запроса

```HTTP

    GET /api/v2/ad_groups.json
```

Пример ответа

```HTTP

    {
        "count": 3,
        "offset": 0,
        "items": [
            {
                "package_id": 83,
                "last_updated": "2022-07-04 17:36:16",
                "id": 6617841,
                "name": "New ad group 2022-07-15 17:53"
            },
            {
                "package_id": 83,
                "last_updated": "2022-07-04 17:36:16",
                "id": 6711647,
                "name": "New ad group 2022-08-16 19:49"
            },
            {
                "package_id": 83,
                "last_updated": "2022-07-04 17:36:16",
                "id": 6711665,
                "name": "New ad group 2022-08-16 19:51"
            }
        ]
    }
```

Доступные поля - описаны в [AdGroup](../object/AdGroup)

Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

- limit - количество групп в ответе. По умолчанию 20

```HTTP

    /api/v2/ad_groups.json?limit=10
```

- offset - смещение на N групп от начала текущей выборки

```HTTP

    /api/v2/ad_groups.json?limit=5&offset=15
```

Фильтры

- _id - ID группы

```HTTP

    /api/v2/ad_groups.json?_id=6617841
    /api/v2/ad_groups.json?_id__in=6617841,6711647
```

- _status - статус группы. Доступные статусы "active", "blocked", "deleted"

```HTTP

    /api/v2/ad_groups.json?_status=active
    /api/v2/ad_groups.json?_status__ne=active
    /api/v2/ad_groups.json?_status__in=active,blocked
```

- _last_updated - datetime последнего обновления группы вместе с баннерами. Доступные ограничения "lt" - меньше, "lte" - меньше или равно, "gt" - больше, "gte" - больше или равно

```HTTP

    /api/v2/ad_groups.json?_last_updated__gt=2022-01-01 00:00:00
    /api/v2/ad_groups.json?_last_updated__gte=2022-01-01 00:00:00
    /api/v2/ad_groups.json?_last_updated__lt=2022-01-01 00:00:00
    /api/v2/ad_groups.json?_last_updated__lte=2022-01-01 00:00:00
```

Сортировка

- id

```HTTP

    /api/v2/ad_groups.json?sorting=id - по возрастанию
    /api/v2/ad_groups.json?sorting=-id - по убыванию
```

- name

```HTTP

    /api/v2/ad_groups.json?sorting=name - по возрастанию
    /api/v2/ad_groups.json?sorting=-name - по убыванию
```

- status

```HTTP

    /api/v2/ad_groups.json?sorting=status - по возрастанию
    /api/v2/ad_groups.json?sorting=-status - по убыванию
```

- по нескольким полям

```HTTP

    /api/v2/ad_groups.json?sorting=status,name,-id

```

### POST

Создание рекламной группы

Пример запроса:

```HTTP

    POST /api/v2/ad_groups.json
    {
        "name": "Моя новая группа",
        "status": "active",
        "date_start": "2022-04-01 00:00:00",
        "date_end": "2022-04-15 00:00:00",
        "autobidding_mode": "second_price",
        "budget_limit_day": "1000",
        "budget_limit": "5000",
        "mixing": "fastest",
        "price": "642.12",
        "age_restrictions": "18+",
        "banner_uniq_shows_limit": 2130,
        "uniq_shows_period": "week",
        "uniq_shows_limit": 100,
        "audit_viewability": "moat",
        "enable_utm": "False",
        "package_id": 449,
        "objective": "playersengagement",
        "banners": [{
            "content": {
                "primary": {
                    "id": 32433493
                }
            },
            "urls": {
                "primary": {
                    "id": 98574325
                }
            },
            "textblocks": {
                "primary": {
                    "title": "Этот товар нужен всем!",
                    "text": "Для счастья нужно только..."
                }
            }
        }, {
            "content": {
                "primary": {
                    "id": 32433494
                }
            },
            "urls": {
                "primary": {
                    "id": 98574325
                }
            },
            "textblocks": {
                "primary": {
                    "title": "Купи меня!",
                    "text": "Купи прямо сейчас"
                }
            }
        }],
        "targetings": {
            "age": {
                "age_list": [21, 22, 23]
            },
            "birthday": {
                "days_after": 5,
                "days_before": 10
            },
            "fulltime": {
                "mon": [1],
                "tue": [1, 2],
                "wed": [1, 2, 3],
                "thu": [1, 2, 3, 4],
                "fri": [1, 2, 3, 4, 5],
                "sat": [1, 2, 3, 4, 5, 6],
                "sun": [1, 2, 3, 4, 5, 6, 7],
                "flags": [],
            },
            "pads": [5206],
            "sex": ["male"],
            "interests": [9018,7356],
            "interests_soc_dem": [7653,7655]
        }
    }
```

Пример ответа:

```HTTP

    HTTP 200
    {
        "id": 9826424,
        "banners": [{
            "id": 23826937
        }]
    }
```

В ответе всегда присутствуют поля id и banners (если группа создается с баннерами).
Важно! banners неподдерживается в fields и возвращается ошибка.

Доступные поля, таргетинги и прочие настройки рекламной группы описываются в [объекте пакета](../object/Package), в рамках которого создаётся группа.

Возможно создавать группу с одним из статусов: active, blocked, deleted.
Если статус не передан, то устанавливается статус active.

Возможные коды ответа

- 200/204 - группа сохранена
- 400 - ошибка валидации

Возможные коды ошибок:

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

Примеры указания таргетингов при создании/редактировании групп

- age:

```HTTP

    {
        "age": {
            "age_list": [0, 12, 13, 14, 22, 23, 24]
        }
    }
```

- birthday:

```HTTP

    {
        "birthday": {
            "days_after": 5,
            "days_before": 10
        }
    }
```

- browser:

```HTTP

    {
        "browser": ["edge", "internet_explorer", "opera"]
    }
```

- fulltime:

```HTTP

    {
        "fulltime": {
            "tue": [2],
            "wed": [2, 3],
            "thu": [2, 3, 4],
            "fri": [2, 3, 4, 5],
            "sat": [2, 3, 4, 5, 6],
            "sun": [2, 3, 4, 5, 6, 7],
            "flags": ["use_holidays_moving", "cross_timezone"],
    }
```

- geo:

```HTTP

    {
        "geo": {
            "regions": [56, 97, 100]
        }
    }
```

или

```HTTP

    {
        "geo": {
            "local_geo": {
                "visit_type": "usual",
                "loc_type": ["home", "work"],
                "locations": [{
                    "lat": 55.75583,
                    "lng": 37.6173,
                    "radius": 3000,
                    "label": "Центр Москвы",
                    "address": "Точный адрес"
                }]
            }
        }
    }
```

Нельзя передавать одновременно local_geo и regions в geo!

Пример некорректного заполнения geo:

```HTTP

    {
        "regions": [56, 97, 100],
        "local_geo": {
            "visit_type": "usual",
            "loc_type": ["home", "work"],
            "locations": [{
                "lat": 55.75583,
                "lng": 37.6173,
                "radius": 3000,
                "label": "Центр Москвы",
                "address": "Точный адрес"
            }]
        }
    }
```

Также вместе с geo нельзя одновременно передавать local_geo и/или regions!

Пример некорректного запроса:

```HTTP

    POST /api/v2/ad_groups/9826424.json
    {
        "targetings": {
            "regions": [56, 97, 100],
            "geo": {
                "regions": [56, 97, 100]
            },
        }
    }
```

- group_members:

```HTTP

    {
        "group_members": "not_group_member"
    }
```

- interests:

```HTTP

    {
        "interests": [9413, 9414, 9415]
    }
```

- interests_soc_dem:

```HTTP

    {
        "interests_soc_dem": [0, 12, 13, 14, 22, 23, 24]
    }
```

- local_geo:

```HTTP

    {
        "local_geo": {
            "visit_type": "usual",
            "loc_type": ["home", "work"],
            "locations": [{
                "lat": 55.75583,
                "lng": 37.6173,
                "radius": 3000,
                "label": "Центр Москвы",
                "address": "Точный адрес"
            }]
        }
    }
```

- mobile_apps:

```HTTP

    {
        "mobile_apps": "deleted"
    }
```

- mobile_operation_systems:

```HTTP

    {
        "mobile_operation_systems": [37, 38, 39]
    }
```

- mobile_operators:

```HTTP

    {
        "mobile_operators": [3, 5, 6]
    }
```

- mobile_prefix:

```HTTP

    {
        "mobile_prefix": ["mts", "beeline", "megafon"]
    }
```

- mobile_types:

```HTTP

    {
        "mobile_types": ["smartphones", "tablets"]
    }
```

- mobile_vendors:

```HTTP

    {
        "mobile_vendors": [14, 41, 49]
    }
```

- pad_category:

```HTTP

    {
        "pad_category": {
            "iOS": [12, 13, 41]
            "Android": [7, 9, 83]
        }
    }
```

- pads:

```HTTP

    {
        "pads": [9863, 9872]
    }
```

- regions:

```HTTP

    {
        "regions": [56, 97, 100]
    }
```

- segments:

```HTTP

    {
        "segments": [22679, 22728]
    }
```

- sex:

```HTTP

    {
        "sex": ["male", "female"]
    }
```

- geo (regions):

```HTTP

    {
        "geo": {
            "regions": [56, 97, 100, 188, -70]
        }
    }
```

- geo (local_geo):

```HTTP

    {
        "geo": {
            "local_geo": {
                "visit_type": "usual",
                "loc_type": ["home", "work"],
                "locations": [{
                    "lat": 55.75583,
                    "lng": 37.6173,
                    "radius": 3000,
                    "label": "Центр Москвы",
                    "address": "Точный адрес"
                }]
            }
        }
    }
```