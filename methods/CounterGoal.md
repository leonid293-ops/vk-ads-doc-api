# CounterGoal

> Оригинал: [https://ads.vk.com/doc/api/resource/CounterGoal](https://ads.vk.com/doc/api/resource/CounterGoal)

---

## /api/v2/remarketing/counters//goals/.json

Ресурс, позволяющий управлять целями счетчика [Top@Mail.ru](https://top.mail.ru).

Используется объект: [RemarketingCounterGoal](../object/RemarketingCounterGoal)

### POST

Запрос редактирует указанную цель счетчика. Для редактирования доступны поля value, name, goal_type.

Пример запроса:

```HTTP

  POST /api/v2/remarketing/counters/2500000/goals/42.json
  {
    "value":45,
    "name":"Добавил в корзину",
    "goal_type":"basket"
  }
```

Пример ответа:

```HTTP

  {
    "value":45,
    "name":"Добавил в корзину",
    "goal_type":"basket"
  }
```

Возвращаемые коды статуса:

200 - Цель успешно изменена.

400 - Ошибка валидации.

404 - Счетчик или цель отсутствует.

Примеры ошибок:

```HTTP

  {"error": {"message": "Can not edit goal for unconfirmed counter"}}
 - Пользователь не является владельцем счетчика, и счетчик не подтвердил доступ к нему.

  {"error": {"message": "Can not edit goal for shared counter"}}
 - Доступ к счетчику был предоставлен пользователю через ключ доступа в VK Ads.
```84:Te0c,