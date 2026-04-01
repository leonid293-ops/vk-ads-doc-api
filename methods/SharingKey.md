# SharingKey

> Оригинал: [https://ads.vk.com/doc/api/resource/SharingKey](https://ads.vk.com/doc/api/resource/SharingKey)

---

## /api/v2/sharing_keys.json

Ресурс, позволяющий создавать [ключи доступа](https://target.my.com/adv/help/shared_sources/) к источникам данных (спискам пользователей, счётчикам и т.п.).

Используется объект: [SharingKey](../object/SharingKey)

### GET

Возвращает список всех ключей доступа, созданных пользователем.

Пример запроса:

```HTTP

   GET /api/v2/sharing_keys.json
```

Дополнительные GET-параметры:

С помощью следующих GET-параметров можно фильтровать данные:

- _key - Ключ.

Пример запроса с дополнительными параметрами:

```HTTP

   GET /api/v2/sharing_keys.json?_key=aBcDe432

```

Пример ответа:

```HTTP

  {
    "items": [
      {
        "sharing_url": "https://ads.vk.com/segments/external/activate_key?key=aBcDe432",
        "sources": [{
             "object_type": "users_list",
             "object_id": 1
          }
        ],
        "price": "0",
        "sharing_key": "aBcDe432",
        "is_marketplace": false,
        "send_email": null,
        "payment_type": "free",
        "owner": {
          "username": "your.user@mail.ru",
          "id": 4000000
        },
        "type": "private",
        "users": [
          {
             "username": "shared.user@mail.ru",
             "id": 4100000
          }
        ]
      },
      {
        "sharing_url": "https://ads.vk.com/segments/external/activate_key?key=fGhKlM765",
        "sources": [
          {
            "object_type": "counter",
            "object_id": 2
          },
          {
            "object_type": "pricelist",
            "object_id": 3
          },
        ],
        "price": "200",
        "sharing_key": "fGhKlM765",
        "is_marketplace": true,
        "send_email": null,
        "payment_type": "fixed_cpm",
        "owner": {
          "username": "your.user@mail.ru",
          "id": 4000000
        },
        "type": "public",
        "users": [
          {
            "username": "shared.user@mail.ru",
            "id": 4100000
          }
        ]
      },
    ]
  }
```

### POST

Создает ключ доступа к источникам данных.

В поле "sources" перечисляются источники, доступ к которым будет предоставляться по этому ключу.
Поддерживаемые типы источников:

* "campaign_list" - рекламные кампании,
* "counter" - счетчики [Top@Mail.ru](https://top.mail.ru),
* "custom_audience" - типовые аудитории,
* "lookalike_audience" - Look-Alike аудитории,
* "pricelist" - продуктовые фиды,
* "segment" - аудиторные сегменты,
* "users_list" - списки пользователей.

Источники можно добавить в ключ при следующих условиях:

* пользователь является владельцем источника;
* для сегментов: пользователь является владельцем всех вложенных источников и сегментов;
* источник не удален пользователем;
* для Look-Alike: Look-Alike аудитория успешно загружена;

В поле "users" перечисляются имена пользователей VK Ads, которые смогут активировать ключ. Вместо имени можно указать e-mail незарегистрированного пользователя. Если оставить поле пустым, ключ будет публичным, и активировать его сможет любой пользователь.

Пример запроса:

```HTTP

  POST /api/v2/sharing_keys.json
  {
    "sources": [
      {
        "object_type": "segment",
        "object_id": 300
      }
    ],
    "send_email": true,
    "users": [{"username": "to.share@mail.ru"}]
  }
```

Пример ответа:

```HTTP

  {
    "users": [{"username": "to.share@mail.ru"}],
    "price": "0",
    "sharing_key": "aBcDe23432",
    "is_marketplace": false,
    "sources": [
      {
        "object_type": "segment",
        "object_id": 300
      }
    ],
    "payment_type": "free",
    "owner": {
      "username": "your.user@mail.ru",
      "id": 4000000
    },
    "type": "private",
    "sharing_url": "https://ads.vk.com/segments/external/activate_key?key=aBcDe23432"
  }
```

Возвращаемые коды статуса:

200 - Ключ был успешно создан.

400 - В следующих случаях:

- Ошибка валидации данных (код "validation_failed").

Примеры ошибок:

- Пользователь не является владельцем источника.

```HTTP

  {"error": {
    "fields": {"sources": {"items": [
      {"code": "unallowed_value",
       "message": "Object not found", 
       "arguments": {"object_id": 59070, "object_type": "segment"}}
    ]}}, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Источник не активен (например, список пользователей, отмеченный к удалению, или Look-Alike аудитория, загрузка которой завершилась с ошибкой).

```HTTP

  {"error": {
    "fields": {"sources": {"items": [
      {"code": "unallowed_value",
       "message": "Object not active", 
       "arguments": {"object_id": 59070, "object_type": "segment"}}
    ]}}, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Источником невозможно поделиться по иной причине.

```HTTP

 {"error": {
    "fields": {"sources": {"items": [
      {"code": "unallowed_value",
       "message": "Object not shareable", 
       "arguments": {"object_id": 59070, "object_type": "segment"}}
    ]}}, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Пользователь не является DMP, ключ нельзя опубликовать в DMP Marketplace.

```HTTP

  {"error": {
    "fields": {"is_marketplace": 
      {"code": "unallowed_value",
       "message": "Only DMP can publish to marketplace", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Пользователь не указал название DMP-провайдера, ключ нельзя опубликовать в DMP Marketplace.

```HTTP

  {"error": {
    "fields": {"is_marketplace": 
      {"code": "unallowed_value",
       "message": "DMP user name has to be set to publish to marketplace", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Ключ приватный, его нельзя опубликовать в DMP Marketplace.

```HTTP

  {"error": {
    "fields": {"is_marketplace": 
      {"code": "unallowed_value",
       "message": "Cannot be set for private keys", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Попытка поделиться приватным ключом с владельцем.

```HTTP

  {"error": {
    "fields": {"users": 
      {"code": "unallowed_value",
       "message": "Cannot assign key to owner", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Невалидные почтовые адреса.

```HTTP

  {"error": {
    "fields": {"users": 
      {"code": "invalid_email",
       "message": "Enter a valid email address or username", 
       "value": ["invalid_email_1", "invalid_email_2"]
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Не указана цена для платного ключа.

```HTTP

  {"error": {
    "fields": {"price": 
      {"code": "required",
       "message": "Price is required for fixed_cpm keys", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Пользователь не является DMP, нельзя создать платный ключ.

```HTTP

  {"error": {
    "fields": {"price": 
      {"code": "invalid_type",
       "message": "Only DMP partner can create CPM keys", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```

- Указана цена для бесплатного ключа.

```HTTP

  {"error": {
    "fields": {"price": 
      {"code": "unallowed_value",
       "message": "Price is only for fixed_cpm keys", 
    }, 
    "message": "Validation failed", 
    "code": "validation_failed"
  }}
```