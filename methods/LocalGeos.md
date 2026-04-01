# LocalGeos

> Оригинал: [https://ads.vk.com/doc/api/resource/LocalGeos](https://ads.vk.com/doc/api/resource/LocalGeos)

---

## /api/v2/remarketing/local_geo.json

Ресурс для управления списками локальной географии. После создания списков их можно включить в сегмент, который можно включить в таргетинг кампании.

Используется объект: [LocalGeo](../object/LocalGeo)

### GET

Получение списка списков локальной географии.
Пример запроса:

```HTTP

   GET /api/v2/remarketing/local_geo.json?fields=id,name,regions
```

Пример ответа:

```HTTP

  {
    "items": [{
      "id": 1,
      "name": "Новый список локальной географии",
      "regions": [{
        "lat": 55.75583,
        "lng": 37.6173,
        "radius": 3000,
        "label": "Центр Москвы",
        "address": "Точный адрес"
      }]
    }]
  }
```

Ответ содержит массив items, состоящий из объектов [LocalGeo](../object/LocalGeo)

### POST

Создание списка локальной географии.

Пример запроса:

```HTTP

    POST /api/v2/remarketing/local_geo.json
  {
    "name": "Новый список локальной географии",
    "regions": [{
      "lat": 55.75583,
      "lng": 37.6173,
      "radius": 3000,
      "label": "Центр Москвы",
      "address": "Точный адрес"
    }]
  }
```

Пример ответа:

```HTTP

  {
    "id": 1,
    "name": "Новый список локальной географии",
    "regions": [{
      "lat": 55.75583,
      "lng": 37.6173,
      "radius": 3000,
      "label": "Центр Москвы",
      "address": "Точный адрес"
    }]
  }
```

Возвращаемые коды статуса:

200 - если список был успешно создан.

400 - в следующих случаях:

- ошибки валидации - код validation_failed;

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": { поля, в которых были найдены ошибки }}}
```