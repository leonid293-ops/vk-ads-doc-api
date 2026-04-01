# RemarketingCounters

> Оригинал: [https://ads.vk.com/doc/api/resource/RemarketingCounters](https://ads.vk.com/doc/api/resource/RemarketingCounters)

---

## /api/v2/remarketing/counters.json

Ресурс, позволяющий управлять счетчиками [Top@Mail.ru](https://top.mail.ru), добавленных пользователем в доступные для использования в целевых аудиториях источники данных. Счетчики используются для настройки таргетинга на пользователей, которые посещали сайт, где он установлен.

Используется объект: [RemarketingCounter](../object/RemarketingCounter)

### GET

Запрос возвращает список всех счетчиков, добавленных пользователем в источники данных.

Пример запроса:

```HTTP

  GET /api/v2/remarketing/counters.json
```

Пример ответа:

```HTTP

  {  
    "items":[  
      {  
        "status":"active",
        "working":true,
        "name":"Счетчик 1",
        "counter_id":2000000,
        "created":"2015-07-31 14:40:12",
        "system_status":"active",
        "flags":[],
        "id":17668
      },
      {  
        "status":"active",
        "working":false,
        "name":"Счетчик 2",
        "counter_id":2500000,
        "created":"2017-03-21 13:25:00",
        "system_status":"active",
        "flags":[  
          "cookie_sync"
        ],
        "id":51645
      }
    ]
  }
```

Фильтры

- _counter_id - ID счетчика в Топ

```HTTP

    /api/v2/remarketing/counters.json?_counter_id=250000
    /api/v2/remarketing/counters.json?_counter_id__in=250000,250001
```

- _domain - домен, к которому привязан счетчик

```HTTP

    /api/v2/remarketing/counters.json?_domain=example.com
    /api/v2/remarketing/counters.json?_domain__in=example.com,example2.com

```

### POST

Запрос создает новый счетчик или добавляет существующий в список доступных источников данных.

Пример запроса на создание нового счетчика:

```HTTP

  POST /api/v2/remarketing/counters.json
  {
    "name":"Новый счетчик",
    "url":"http://example.com",
    "email":"test@example.com",
    "password":"12345678"
  }
```

Пример запроса на добавление существующего счетчика в источники данных:

```HTTP

  POST /api/v2/remarketing/counters.json
  {
    "counter_id": 2000500,
    "name":"Новый счетчик",
    "flags": ["cookie_sync"]
  }
```

Добавить счётчик может только владелец счётчика (email-адрес владельца счётчика совпадает с email-адресом аккаунта VK Ads) либо пользователь, который имеет доступ к этому счётчику (владелец может дать доступ к счётчику, указав в своем профиле VK Ads email-адрес другого пользователя). Если у вас нет доступа к счётчику, который вы добавляете, он будет зарегистрирован как неактивный ("system_status" = "blocked"), а владельцу будет отправлен запрос на подтверждение. В случае получения разрешения владельца счётчик будет активирован автоматически.

Пример ответа:

```HTTP

  {  
    "status":"active",
    "working":null,
    "name":"Новый счетчик",
    "counter_id":2000000,
    "created":"2015-07-31 14:40:12",
    "system_status":"active",
    "flags":[],
    "id":17668
  }
```

Возвращаемые коды статуса:

200 - Счетчик успешно добавлен.

400 - Одно из следующих событий:

- Ошибка валидации. Код "validation_failed".
- Попытка добавления уже подключённого счётчика. Код "duplicate_error".
- Ошибка при создании нового счётчика в [Top@Mail.ru](https://top.mail.ru). Код "top_error".

404 - Счетчик с указанным в запросе counter_id не существует. Ошибка возникает при добавлении счетчика.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": {  }}}
 - Ошибка в значениях передаваемых данных.

  {"error": {"code": "duplicate_error", "message": "Counter with counter_id 12345 already exists"}}
 - Попытка добавления уже подключённого счётчика.

  {"error": {"code": "top_error", "message": ""}}
 - Ошибка при создании нового счётчика в [Top@Mail.ru](https://top.mail.ru).
```