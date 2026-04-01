# BannerRemoderation

> Оригинал: [https://ads.vk.com/doc/api/resource/BannerRemoderation](https://ads.vk.com/doc/api/resource/BannerRemoderation)

---

## /api/v2/banners/remoderate.json

Ресурс, позволяющий отправить баннер на перемодерацию.

### POST

Пример запроса:

```HTTP

   POST /api/v2/banners/remoderate.json?fields=id,remoderated

    {
        "banners": [
            {
                "id": 1527521
            },
            {
                "id": 6543425
            }
        ]
    }
```

Пример ответа:

```HTTP

    {
        "banners": [
            {
                "id": 1527521,
                "remoderated": False
            },
            {
                "id": 6543425,
                "remoderated": True
            }
        ]
    }
```

В ответе содержится поле `remoderated`, которое указывает, была ли отправка на перемодерацию успешной.

Обратите внимание, что не все баннеры могут быть отправлены на перемодерацию. 
Чтобы узнать, какие баннеры можно отправить на перемодерацию, достаточно запросить [АПИ баннеров](../resource/Banners)  с полями `id` и `user_can_request_remoderation`. При `user_can_request_remoderation = True` баннер можно отправить на перемодерацию.9f:T15e8,