# Banners

> Оригинал: [https://ads.vk.com/doc/api/resource/Banners](https://ads.vk.com/doc/api/resource/Banners)

---

## /api/v2/banners.json

Ресурс, позволяющий создать или получить список всех рекламных объявлений пользователя.

Используется объект: [Banner](../object/Banner)

### GET

Получение списка рекламных объявлений

Пример запроса

```HTTP

    GET /api/v2/banners.json
```

Пример ответа

```HTTP

    {
        "count": 3,
        "offset": 0,
        "items": [
            {
                "id": 23826937
                "ad_group_id": 9367343
            },
            {
                "id": 23826938
                "ad_group_id": 9367343
            },
            {
                "id": 24582643
                "ad_group_id": 9401602
            }
        ]
    }
```

Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

- limit - количество объектов в ответе. По умолчанию 20

```HTTP

    GET /api/v2/banners.json?limit=10
```

- offset - смещение на N объектов от начала текущей выборки

```HTTP

    GET /api/v2/banners.json?limit=5&offset=15
```

Фильтры

- _id - ID объявления

```HTTP

    /api/v2/banners.json?_id=26617841
    /api/v2/banners.json?_id__in=26617841,26711647
```

- _ad_group_id - ID рекламной группы

```HTTP

    /api/v2/banners.json?_ad_group_id=6617841
    /api/v2/banners.json?_ad_group_id__in=6617841,6711647
```

- _ad_group_status - статус рекламной группы. Доступные статусы "active", "blocked", "deleted"

```HTTP

    /api/v2/banners.json?_ad_group_status=active
    /api/v2/banners.json?_ad_group_status__ne=active
    /api/v2/banners.json?_ad_group_status__in=active,blocked
```

- _status - статус объявления. Доступные статусы "active", "blocked", "deleted"

```HTTP

    /api/v2/banners.json?_status=active
    /api/v2/banners.json?_status__ne=active
    /api/v2/banners.json?_status__in=active,blocked
```

- _updated - datetime последнего обновления объявления. Доступные ограничения "lt" - меньше, "lte" - меньше или равно, "gt" - больше, "gte" - больше или равно

```HTTP

    /api/v2/banners.json?_updated__gt=2022-01-01 00:00:00
    /api/v2/banners.json?_updated__gte=2022-01-01 00:00:00
    /api/v2/banners.json?_updated__lt=2022-01-01 00:00:00
    /api/v2/banners.json?_updated__lte=2022-01-01 00:00:00
```

- _url - полнотекстовый регистрозависимый поиск по ссылкам баннера

```HTTP

    /api/v2/banners.json?_url=mail.ru

```

- _textblock - полнотекстовый регистрозависимый поиск по содержимому текстблоков баннера

```HTTP

    /api/v2/banners.json?_textblock=купить насос
```