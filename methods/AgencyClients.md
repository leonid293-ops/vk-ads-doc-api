# AgencyClients

> Оригинал: [https://ads.vk.com/doc/api/resource/AgencyClients](https://ads.vk.com/doc/api/resource/AgencyClients)

---

## /api/v2/agency/clients.json

Ресурс позволяет получить информацию о существующих клиентах агентства и создать новых.

Ресурс доступен только пользователям-агентствам.

Используется объект: [AgencyClient](../object/AgencyClient)

### GET

Запрос возвращает список всех клиентов, находящихся в ведении агентства.

Пример запроса:

```HTTP

   GET /api/v2/agency/clients.json
```

Дополнительные GET-параметры:

С помощью следующих GET-параметров можно фильтровать данные:

- limit - Количество возвращаемых в ответе клиентов. Значение по умолчанию: 20. Максимальное значение: 50.
- offset - Смещение точки отсчета относительно начала списка клиентов. Значение по умолчанию: 0.
- _user__id - Идентификатор клиента.
- _user__id__in - Список идентификаторов клиента через запятую.
- _user__username - Имя клиента.
- _user__username__in - Список имен клиентов через запятую. Имена задаются в формате "username1,username2,...,usernameN".
- _user__status, _user__status__ne - Статус клиента.
- _user__status__in - Список статусов через запятую.
- _status, _status__ne - Статус отношения между клиентом и агенством.
- _status__in - Список статусов через запятую.
- _q - полнотекстовый поиск по user.username, user.additional_info.client_name, user.additional_info.client_info  
- \_is_vkads - признак клиента ВК Рекламы

Пример запроса с дополнительными параметрами:

```HTTP

   GET /api/v2/agency/clients.json?limit=50&offset=100&_user__username=Василий Иванов
```

Пример ответа:

```HTTP

    {
        "count": 1,
        "items": [
            {
                "access_type": "full_access",
                "status": "active",
                "user": {
                   "account": {
                      "id": 17668,
                      "balance": 3000,
                      "a_balance": 0,
                      "type": "physical",
                      "currency_balance_hold": 300,
                   },
                   "additional_emails": ["test@mail.ru"],
                   "additional_info": {
                      "name": "Василий Иванов",
                      "email": "test@example.com",
                      "phone": "89153724330",
                      "address": "",
                      "client_info": "Заметка",
                      "client_name": "Василий Иванов",
                   },
                   "id": 17668,
                   "status": "active",
                   "username": "Василий Иванов",
                },
            },
            ...
       ],
       "limit": 20,
       "offset": 0
   }
```

### POST

Запрос создает нового клиента или добавляет существующего в список клиентов, находящихся в ведении агентства.
Привязать существующего клиента можно только если учетная запись отвечает следующим условиям:
- находится в статусе "active";
- является прямым рекламодателем;
- не привязана к какому-либо агентству или представительству;
- использует валюту агентства ([User](../object/User).currency).

Пример запроса на создание нового клиента:

```HTTP

  POST /api/v2/agency/clients.json
  {
    "access_type":"full_access",
    "user": {
      "additional_emails": ["test@mail.ru"],
      "additional_info": {
        "client_info": "Заметка",
        "client_name": "Василий Иванов",
      }
    }
  }
```

Пример запроса на добавление существующего клиента:

```HTTP

  POST /api/v2/agency/clients.json
  {
    "access_type":"full_access",
    "user": {
      "id":17668,
      "additional_emails": ["test@mail.ru"],
      "additional_info": {
        "client_info": "Заметка",
        "client_name": "Василий Иванов",
      }
    }
  }

```
Пример запроса на добавление существующего клиента c использованием username:
```HTTP

  POST /api/v2/agency/clients.json
  {
    "access_type":"full_access",
    "user": {
      "username":"client_username",
      "additional_emails": ["test@mail.ru"],
      "additional_info": {
        "client_info": "Заметка",
        "client_name": "Василий Иванов",
      }
    }
  }

```

Пример ответа:

```HTTP

  {
    "user": {
      "id":17668,
      "username":"client_username"
    }
  }
```

Также нужно обязательно передавать данные для регистрации в ОРД в зависимости от типа клиента. Для этого используйте поле "physical_details" (для физ.лиц) или "juridical_details" (для юр.лиц). В массиве "sub_agents" передаются данные подрядчиков между клиентом и агентством:

- данные договора с клиентом передаются в основных полях "physical_details" или "juridical_details"
- если клиент работает непосредственно с агентством, то "sub_agents" должен быть пустым или null
- порядок элементов в массиве важен, он определяет цепочку договоров между подрядчиками и заканчивается данными между последним из них и агентством

```HTTP
{
 "physical_details": {
    "phone": "string",
    "user_type": "foreign_physical",
    "name": "string",
    "inn": "string",
    "contract_number": "string",
    "contract_date": "2022-08-31",
    "contract_type": "additional",
    "contract_subject": "representation",
    "vat": true,
    "sub_agents": [
      {
        "user_type": "physical",
        "name": "string",
        "inn": "string",
        "contract_number": "string",
        "contract_date": "2022-08-31",
        "contract_type": "additional",
        "contract_subject": "representation",
        "vat": true
      }
    ]
  }

  "juridical_details": {
    "user_type": "foreign_juridical",
    "name": "string",
    "inn": "string",
    "contract_number": "string",
    "contract_date": "2022-08-31",
    "contract_type": "additional",
    "contract_subject": "representation",
    "vat": true,
    "sub_agents": [
      {
        "user_type": "physical",
        "name": "string",
        "inn": "string",
        "contract_number": "string",
        "contract_date": "2022-08-31",
        "contract_type": "additional",
        "contract_subject": "representation",
        "vat": true
      }
    ]
  }

```

Возвращаемые коды статуса:

200 - Клиент был успешно добавлен.

400 - В следующих случаях:

- Ошибка валидации (код "validation_failed").
- Клиент неактивен или уже привязан какому-либо агентству (код "invalid_user").
- Клиент и агентство используют разную валюту (код "invalid_user").
- Список дополнительных email адресов содержат основной email адрес пользователя (код "duplicate_value")

404 - Клиент с указанным ID не существует.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": {  }}}
 - Ошибка в значениях передаваемых данных.

  {"error": {"fields": {"user": {"code": "invalid_user", "message": "Cant join agency"}}}}
 - Попытка добавления уже привязанного клиента.

  {"error": {"fields": {"user": {"code": "invalid_user", "message": "Different currency for agency and client"}}}}
 - Попытка добавления клиента, использующего валюту, отличную от валюты агентства.

  {"error": {"fields": {"additional_emails": {"code": "duplicate_value", "message": "Additional emails contain the main user email"}}, "message": "Validation failed", "code": "validation_failed"}}
- Попытка добавления дополнительного email адреса дублирующего основной email адрес пользователя.
```