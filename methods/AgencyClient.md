# AgencyClient

> Оригинал: [https://ads.vk.com/doc/api/resource/AgencyClient](https://ads.vk.com/doc/api/resource/AgencyClient)

---

## /api/v2/agency/clients/&lt;id&gt;.json

Ресурс позволяет управлять учетными записями клиентов агентства.

Ресурс доступен только пользователям-агентствам.

Используется объект: [AgencyClient](../object/AgencyClient)

### POST

Запрос редактирует данные и права доступа клиента агентства.

Пример запроса на редактирование информации о клиенте:

```HTTP

  POST /api/v2/agency/clients/17668.json
  {
    "is_vkads": true,
    "access_type":"full_access",
    "user": {
      "additional_emails": ['test@mail.ru'],
      "additional_info": {
        "client_info": "Заметка",
        "client_name": "Василий Иванов",
      }
    }
  }
```

гдe 17668 - это ID клиента.

Возвращаемые коды статуса:

204 - Данные клиента успешно изменены.

400 - Ошибка валидации.

404 - Клиент не найден.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": {  }}}
 - Ошибка в значениях передаваемых данных.
```

### DELETE

Запрос выводит клиента (удаляет) из ведома агентства. Операцию можно произвести только с учетной записью клиента, где баланс меньше или равен нулю и используемая валюта совпадать с валютой агентства ([User](../object/User).currency). Операция не приводит к удалению учетной записи клиента из системы VK Ads.

Пример запроса:

```HTTP

  DELETE /api/v2/agency/clients/17668.json
```

гдe 17668 - это ID клиента.

Возвращаемые коды статуса:

204 - Клиент успешно удален.

400 - В следующих случаях:

- Баланс клиента больше нуля (код "invalid_user").
- Клиент и агентство используют разную валюту (код "invalid_user").

404 - Клиент не найден.

Примеры ошибок:

```HTTP

  {"error": {"fields": {"user": {"code": "invalid_user", "message": "Can't delete client with amount on hold"}}}}
 - Попытка удаления клиента с балансом больше нуля.

  {"error": {"fields": {"user": {"code": "invalid_user", "message": "Can't delete client, money transfer error"}}}}
 - Попытка удаления клиента, использующего валюту, отличную от валюты агентства.
```