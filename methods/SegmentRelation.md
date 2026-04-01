# SegmentRelation

> Оригинал: [https://ads.vk.com/doc/api/resource/SegmentRelation](https://ads.vk.com/doc/api/resource/SegmentRelation)

---

## /api/v2/remarketing/segments//relations/.json

Ресурс, позволяющий изменять параметры источника данных в сегменте аудитории.

Используется объект: [SegmentRelation](../object/SegmentRelation)

### POST

Запрос изменяет параметры источника данных в сегменте аудитории. Изменять можно только значения из поля "params".

Пример запроса:

```HTTP

  POST /api/v2/remarketing/segments/243/relations/30.json
```

```HTTP

  { 
    "params": {
      "left": 359, 
      "right": 1, 
      "type": "negative"
    }
  }

```

Пример ответа:

```HTTP

  {"object_type": "remarketing_pricelist", "id": 1120, "object_id": 30}
```

Возвращаемые коды статуса:

200 - Источник успешно изменен.
400 - Ошибка валидации.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "message": "Left should be greater than right"}}
```

### DELETE

Запрос удаляет источник данных из сегмента аудитории.

Пример запроса:

```HTTP

  DELETE /api/v2/remarketing/segments/243/relations/30.json
```

Возвращаемые коды статуса:

204 - Источник данных успешно удален.
400 - В результате удаления источника данных, их количество в сегменте стало меньше "pass_condition". Требуется уменьшить значение "pass_condition" для нужного сегмента и отправить запрос еще раз.
404 - Сегмент или источник данных отсутствуют.96:Te82,