# AppleApp

> Оригинал: [https://ads.vk.com/doc/api/resource/AppleApp](https://ads.vk.com/doc/api/resource/AppleApp)

---

## /api/v2/apple_apps/.json

Ресурс, предоставляющий информацию о мобильном приложении из App Store.

### GET

Запрос возвращает информацию о мобильном приложении из App Store.

Пример запроса:

```HTTP

  GET /api/v2/apple_apps/535176909.json
```

Пример ответа:

```HTTP

    {
        "id": 5,
        "name": "535176909",
        "type": "game",
        "category_id": 4,
        "content_rating": "9+",
        "title": "BADLAND",
        "description": "Some words about app.",
        "icon_image": 
            {
                "preview_url": "http://rbui.trgqa.devmail.ru/img/39/6AFC7B.jpg",
                "height": 256,
                "width": 256,
                "content_id": 2141189,
                "type": "static",
                "id": 21966770,
                "size": 59566
            }
    }

```

Возвращаемые коды статуса:

404 - Мобильное приложение не найдено.

### POST

Запрос обновляет информацию о мобильном приложении из App Store.

Пример запроса:

```HTTP

  POST /api/v2/apple_apps/535176909.json
```

Пример ответа:

```HTTP

    {
        "id": 5,
        "name": "535176909",
        "type": "game",
        "category_id": 4,
        "content_rating": "9+",
        "title": "BADLAND",
        "description": "Some words about app.",
        "icon_image": 
            {
                "preview_url": "http://rbui.trgqa.devmail.ru/img/39/6AFC7B.jpg",
                "height": 256,
                "width": 256,
                "content_id": 2141189,
                "type": "static",
                "id": 21966770,
                "size": 59566
            }
    }

```

Возвращаемые коды статуса:

404 - Мобильное приложение не найдено.7e:T9e4,