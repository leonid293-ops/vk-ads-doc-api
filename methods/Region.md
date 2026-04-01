# Region

> Оригинал: [https://ads.vk.com/doc/api/resource/Region](https://ads.vk.com/doc/api/resource/Region)

---

## /api/v2/regions.json

Ресурс, позволяющий получать информацию о географических регионах.

Используется объект: [Region](../object/Region)

### GET

Запрос возвращает данные о регионах.

Пример запроса:

```HTTP

  GET /api/v2/regions.json
```

Пример ответа:

```HTTP

  {
    "count": 5561,
    "items": [
       {
           "parent_id": -1,
           "id": 188,
           "name": "Россия",
           "flags": ["rb_active","geo_tree_extended","geo_tree"]
       }, {
           "parent_id": 188,
           "id": 53,
           "name": "Краснодарский край",
           "flags": ["rb_active","geo_tree_extended","geo_tree"]
       }, {
           ...
       }
    ]
  }
```

Фильтры

- _id - ID региона

```HTTP

    /api/v2/regions.json?_id=53
    /api/v2/regions.json?_id__in=53,188
```

- _parent_id - ID родительского региона

```HTTP

    /api/v2/regions.json?_parent_id=-1
    /api/v2/regions.json?_parent_id__in=-1,188
```

- _q - полнотекстовый поиск по имени региона

```HTTP

    /api/v2/regions.json?_q=Сочи
```

- _flags - поиск по флагам региона. Возможные значения: geo_tree, geo_tree_extended, rb_active. Поиск по нескольким флагам находит те регионы, у которых есть все указанные флаги

```HTTP

    /api/v2/regions.json?_flags=geo_tree_extended
    /api/v2/regions.json?_flags__in=geo_tree_extended,rb_active
```

В API [пакетов](../resource/Packages) в поле options может приходить следующая структура:

```HTTP

   "items": [
       {
           "id": 613
           "options": [
              {
                  "targetings": [
                      {
                          "name": "regions",
                          "filter": {
                              "flags": ["geo_tree", "rb_active"]
                          }
                      }
                  ]
              }
           ]
       }
   ]
```

Это означает, что в пакете 613 разрешены регионы, у которых есть флаги "geo_tree" и "rb_active". Чтобы получить список таких регионов, нужно запросить API с фильтром по указанным флагам. В данном случае это будет следующий запрос: 

```HTTP

    /api/v2/regions.json?_flags__in=geo_tree,rb_active
```

API поддерживает HTTP заголовок "Accept-Language". В случае непустого значения данные возвращаются на наиболее предпочитаемом поддержанном языке.

На данный момент поддержаны следующие языки: русский, английский. По умолчанию данные отдаются на английском языке. Например:

- При "Accept-Language" = "" данные будут возвращены на английском языке; 

- При "Accept-Language" = "ru-RU,ru;q=0.9,en-US;q=0.8" данные будут возвращены на русском языке; 

- При "Accept-Language" = "de,en-US;q=0.8,ru;q=0.5" данные будут возвращены на английском языке.