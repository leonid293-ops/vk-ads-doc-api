# Segment

> Оригинал: [https://ads.vk.com/doc/api/resource/Segment](https://ads.vk.com/doc/api/resource/Segment)

---

## /api/v2/remarketing/segments/.json

Ресурс, позволяющий управлять сегментом аудитории.

Используется объект: [Segment](../object/Segment)

### GET

Запрос возвращает информацию о сегменте аудитории.

Пример запроса:

```HTTP

  GET /api/v2/remarketing/segments/243.json
```

Пример ответа:

```HTTP

  {
    "id": 243,
    "created": "2017-07-31 14:40:12",
    "updated": "2017-07-31 15:00:50",
    "name": "Мой сегмент",
    "pass_condition": 2
  }
```

### POST

Запрос изменяет параметры сегмента аудитории.

Пример запроса:

```HTTP

  POST /api/v2/remarketing/segments/243.json
```

```HTTP

  {
    "name": "сегмент v2", 
    "pass_condition": 1
  }
```

Пример ответа:

```HTTP

    {
      "id": 243,
      "created": "2017-07-31 14:40:12",
      "updated": "2017-07-31 15:00:50",
      "name": "сегмент v2",
      "pass_condition": 1
    }
```

Возвращаемые коды статуса:

201 - Сегмент успешно создан.
400 - Ошибка валидации.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": {"pass_condition": {"code": "invalid_condition", "message": "Segment pass condition cannot be greater that number of segment relations"}}}}
```

### DELETE

Запрос удаляет сегмент аудитории. Удаление возможно только если сегмент не используется ни в одной кампании и не вложен в другие сегменты.

Пример запроса:

```HTTP

  DELETE /api/v2/remarketing/segments/243.json
```

Возвращаемые коды статуса:

204 - Сегмент успешно удален.
404 - Сегмент отсутствует.
409 - Сегмент задействован в кампаниях пользователя или других сегментах.