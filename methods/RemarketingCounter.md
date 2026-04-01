# RemarketingCounter

> Оригинал: [https://ads.vk.com/doc/api/resource/RemarketingCounter](https://ads.vk.com/doc/api/resource/RemarketingCounter)

---

## /api/v2/remarketing/counters/.json

Ресурс, позволяющий управлять счетчиком [Top@Mail.ru](https://top.mail.ru). Счетчики используются для настройки таргетинга на пользователей, которые посещали сайт, где он установлен.

Используется объект: [RemarketingCounter](../object/RemarketingCounter)

### GET

Запрос возвращает данные об указанном счетчике.

Пример запроса:

```HTTP

  GET /api/v2/remarketing/counters/2000000.json
```

Пример ответа:

```HTTP

  {  
    "status":"active",
    "working":true,
    "name":"Счетчик раз",
    "counter_id":2000000,
    "created":"2015-07-31 14:40:12",
    "system_status":"active",
    "flags":[],
    "id":17668
  }
```

### POST

Запрос изменяет параметры указанного счетчика.

Пример запроса:

```HTTP

  POST /api/v2/remarketing/counters/2000000.json
  {
    "name":"Новое название",
    "flags":["cookie_sync"],
  }
```

где "2000000" - это поле "counter_id" счетчика.

Пример ответа:

```HTTP

  {  
    "status":"active",
    "working":null,
    "name":"Новое название",
    "counter_id":2000000,
    "created":"2015-07-31 14:40:12",
    "system_status":"active",
    "flags":["cookie_sync"],
    "id":17668
  }
```

Возвращаемые коды статуса:

200 - Счетчик успешно изменен.

400 - Ошибка валидации.

404 - Счетчик отсутствует.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": {  }}}
 - Ошибка в значениях передаваемых данных
```

### DELETE

Запрос удаляет указанный счетчик из доступных источников данных. Удаление возможно только если счетчик не используется ни в одной аудитории и на его основе не создано ни одно lookalike-расширение.

Пример запроса:

```HTTP

  DELETE /api/v2/remarketing/counters/2000000.json
```

где "2000000" - это поле "counter_id" счетчика.

Возвращаемые коды статуса:

204 - Счетчик удален.

404 - Счетчик отсутствует.

409 - Счетчик задействован в аудиториях или lookalike пользователя.