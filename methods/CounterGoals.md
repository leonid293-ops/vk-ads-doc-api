# CounterGoals

> Оригинал: [https://ads.vk.com/doc/api/resource/CounterGoals](https://ads.vk.com/doc/api/resource/CounterGoals)

---

## /api/v2/remarketing/counters//goals.json

Ресурс, позволяющий управлять целями счетчика [Top@Mail.ru](https://top.mail.ru).

Используется объект: [RemarketingCounterGoal](../object/RemarketingCounterGoal)

### GET

Запрос возвращает список всех целей указанного счетчика.

Пример запроса:

```HTTP

  GET /api/v2/remarketing/counters/2500000/goals.json
```

Пример ответа:

```HTTP

  {"items": [
    {  
      "substr":"/order",
      "value":null,
      "name":"Корзина",
      "condition":"uss",
      "goal_type":"checkout"
    },
    {  
      "substr":"order_accepted",
      "value":45,
      "name":"Совершил покупку",
      "condition":"jse",
      "goal_type":"purchase"
    },
  ]}
```

### POST

Запрос создает цель указанного счетчика.

Пример запроса:

```HTTP

  POST /api/v2/remarketing/counters/2500000/goals.json
  {  
    "substr":"order_accepted",
    "value":45,
    "name":"Совершил покупку",
    "condition":"jse",
    "goal_type":"purchase"
  }
```

Пример ответа:

```HTTP

  {  
    "substr":"order_accepted",
    "value":45,
    "name":"Совершил покупку",
    "condition":"jse",
    "goal_type":"purchase"
  }
```

Возвращаемые коды статуса:

200 - Цель успешно добавлена.

400 - Ошибка валидации.

404 - Счетчик отсутствует.

Примеры ошибок:

```HTTP

  {"error": {"message": "Can not create goal for unconfirmed counter"}}
 - Пользователь не является владельцем счетчика, и счетчик не подтвердил доступ к нему.

  {"error": {"message": "Can not create goal for shared counter"}}
 - Доступ к счетчику был предоставлен пользователю через ключ доступа в VK Ads.
```