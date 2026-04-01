# Goals

> Оригинал: [https://ads.vk.com/doc/api/resource/Goals](https://ads.vk.com/doc/api/resource/Goals)

---

## /api/v2/goals.json

Ресурс позволяет получить список всех целей, доступных для таргетирования или получения статистики. Список содержит цели счётчиков [Top@Mail.ru](https://top.mail.ru), действий для приложений и групп социальных сетей и установки мобильных приложений.

Используется объект: [Goals](../object/Goals)

### GET

Запрос возвращает список всех доступных целей.

Пример запроса:

```HTTP

  GET /api/v2/goals.json
```

Пример ответа:

```HTTP

    {  
      "ok_game":[  
        {  
          "goal":"ok_game_join",
          "description":"Установка приложения OK"
        }
      ],
      "ok_group":[  
        {  
          "goal":"ok_group_join",
          "description":"Вступление в группу OK"
        }
      ],
      "mobile_install":[  
        {  
          "goal":"mobile_app",
          "description":"Установка приложения"
        }
      ],
      "topmailru":[  
        {  
          "counter_name":"Счетчик Top.Mail.Ru",
          "goal":"uss:goal_1",
          "counter_id":8,
          "id":1,
          "description":"Цель 1"
        },
        {  
          "counter_name":"Счетчик Top.Mail.Ru",
          "goal":"uss:goal_2",
          "counter_id":8,
          "id":2,
          "description":"Цель 2"
        }
      ]
    }
```86:T81f,