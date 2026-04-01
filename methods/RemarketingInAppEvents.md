# RemarketingInAppEvents

> Оригинал: [https://ads.vk.com/doc/api/resource/RemarketingInAppEvents](https://ads.vk.com/doc/api/resource/RemarketingInAppEvents)

---

## /api/v2/remarketing/inapp_events.json

Ресурс позволяет получить список событий в мобильных приложениях, доступных для использования в целевых аудиториях. События можно использовать для настройки таргетинга на пользователей, уже установивших приложение и совершивших/не совершивших в нем определенных действий, которые вы можете отследить с помощью трекера мобильных приложений.

Используется объект: [RemarketingInAppEvent](../object/RemarketingInAppEvent)

### GET

Запрос возвращает список всех событий в мобильных приложениях, доступных для добавления в сегменты аудиторий.

Пример запроса:

```HTTP

  GET /api/v2/remarketing/inapp_events.json
```

Пример ответа:

```HTTP

  [  
    {  
      "app_name":"Android test",
      "trackers":[  
        {  
          "events":[  
            {  
              "id":1,
              "name":"purchase"
            },
            {  
              "id":2,
              "name":"addToCart"
            }
          ],
          "id":133,
          "name":"myTracker"
        },
        {  
          "events":[  
            {  
              "id":3,
              "name":"viewItem"
            }
          ],
          "id":233,
          "name":"anotherTracker"
        }
      ],
      "url":"https://play.google.com/store/apps/details?id=com.test",
      "created":"2018-04-15 22:42:25",
      "platform":"android",
      "url_object_id":"com.test",
      "rb_mobile_app_id":1,
      "status":"new"
    },
    {  
      "app_name":"IOS test",
      "trackers":[  
        {  
          "events":[  
            {  
              "id":1,
              "name":"purchase"
            },
            {  
              "id":2,
              "name":"addToCart"
            }
          ],
          "id":133,
          "name":"myTracker"
        },
        {  
          "events":[  
            {  
              "id":3,
              "name":"viewItem"
            }
          ],
          "id":233,
          "name":"anotherTracker"
        }
      ],
      "url":"https://itunes.apple.com/ru/app/id12345",
      "created":"2018-04-15 22:42:25",
      "platform":"ios",
      "url_object_id":"12345",
      "rb_mobile_app_id":2,
      "status":"approved"
    }
  ]
```

Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

- limit - количество объектов в ответе. По умолчанию 20

```HTTP

    GET /api/v2/remarketing/inapp_events.json?limit=10
```

- offset - смещение на N объектов от начала текущей выборки

```HTTP

    GET /api/v2/remarketing/inapp_events.json?limit=5&offset=15
```

Фильтры

- _url_object_id - ID связанного объекта

```HTTP

    /api/v2/remarketing/inapp_events.json?_url_object_id=com.test
```