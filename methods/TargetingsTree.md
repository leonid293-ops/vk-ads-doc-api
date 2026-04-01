# TargetingsTree

> Оригинал: [https://ads.vk.com/doc/api/resource/TargetingsTree](https://ads.vk.com/doc/api/resource/TargetingsTree)

---

## /api/v2/targetings_tree.json

Ресурс, позволяющий собрать информацию о полном дереве интересов пользователей. Отдельные интересы могут быть доступны не во всех пакетах.

Используется объект: [TargetingsTree](../object/TargetingsTree)

### GET

Пример запроса:

```HTTP

   GET /api/v2/targetings_tree.json
```

Пример ответа:

```HTTP

   [
       {
            "interests_short": [
               {
                   "children": [
                       {
                           "id": 8490,
                           "name": "Дачная жизнь"
                       },
                       {
                           "id": 10255,
                           "name": "Пчеловодство"
                       },
                       {
                           "id": 10257,
                           "name": "Садовые принадлежности"
                       },
                       {
                           "id": 10256,
                           "name": "Семена и рассада"
                       }
                   ],
                   "id": 7299,
                   "name": "Для дома и дачи"
               },
               {
                   "children": [
                       {
                           "id": 9291,
                           "name": "Аквариум"
                       } 
                   ],
                   "id": 7304,
                   "name": "Домашние животные"
               }
            ],
            "interests_soc_dem": [
               {
                   "children": [
                       ...
                   ],
                   "id": 7328,
                   "name": "Группы телесмотрения"
               },
               ...
            ],
            "interests_stable": [
               ...
            ],
            "interests": [
               ...
            ]
       }
   ]
```

По умолчанию в ответе присутствуют 4 поля:
- "interests" (интересы)
- "interests_soc_dem" (расширенные социально-демографические характеристики)
- "interests_stable" (устойчивые долгосрочные интересы)
- "interests_short" (краткосрочные интересы)
Чтобы получить отдельные поддеревья интересов, используйте опциональный параметр "targetings", в качестве значения которого используется строка, содержащая указанные через запятую названия поддеревьев: "interests", "interests_stable", "interests_short", "interests_soc_dem".

Пример запроса:

```HTTP

   GET /api/v2/targetings_tree.json?targetings=interests_soc_dem,interests_short
```

Пример ответа:

```HTTP

   [
       {
            "interests_short": [
               ...
            ],
            "interests_soc_dem": [
               ...
            ]
       }
   ]
```