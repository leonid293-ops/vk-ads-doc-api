# LeadForm

> Оригинал: [https://ads.vk.com/doc/api/resource/LeadForm](https://ads.vk.com/doc/api/resource/LeadForm)

---

## /api/v1/lead_ads/lead_forms/.json

Ресурс, позволяющий получать и обновлять лид формы.

### GET

Получение одной лид формы

Пример запроса

```HTTP

    GET /api/v1/lead_ads/lead_forms/17.json
```

Пример ответа

```HTTP

    {
        "id": "17",
        "name": "Моя первая лидформа"
    }

```

Доступные поля - описаны в [LeadForm](../object/LeadForm)

Параметры

- get_active_form_ad_plans - флаг, указывающий, нужно ли возвращать id активных ad_plan'ов для формы. Если не указан, то по умолчанию они не возвращаются

```HTTP

    /api/v1/lead_ads/lead_forms/17.json?get_active_form_ad_plans=1
```

### POST

Редактирование лид формы

Пример запроса

```HTTP

    POST /api/v1/lead_ads/lead_forms/17.json
    {
        "name": "VK реклама. Обновленная лид форма"
    }
```

Пример ответа

```HTTP

    HTTP 200
    {
        "id": "17",
        "name": "VK реклама. Обновленная лид форма",
        ...
    }
```

Содержимое секций contact_fields, result_info, agreement, notifications и pages полностью замещается при обновлении. К примеру, для лид формы с contact_fields:

```HTTP

    {
        "contact_fields": [
            "first_name",
            "phone",
            "city"
        ],
    }
```

запрос обновления: 

```HTTP

    {
        "contact_fields": [
            "first_name",
            "phone",
            "birth_date"
        ],
    }
```

приведет ровно к такому новому содержимому секцию после обновления.

Возможные коды ответа

- 200 - объявление сохранено
- 400 - ошибка валидации
- 404 - лид форма не найдена

Возможные коды ошибок

- bad_value - неправильный формат или тип значения
- required - поле обязательно
- required_value - ожидается обязательное значение
- unallowed_value - значение не входит в список достимых
- bad_items - в списке присутствуют неправильные значения
- max_value - длина/размер строки/списка больше максимального
- min_value - длина/размер строки/списка меньше минимального
- duplicate_value - в списке встречаются повторяющиеся значения
- bad_contact_field_value - предоставленный список контактных полей не содержит всех необходимых значений

В общем случае сообщение о ошибке имеет следующий формат:

```HTTP

    {
        "error": {
            "fields": {
                "": {
                    "message": "",
                    "code": ""
                },
                "": {
                    "message": "",
                    "code": ""
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```

где field_name_N - название поля, в котором произошла ошибка, error_message_N - описание ошибки, error_code_2 - код ошибки.

Пример:

```HTTP

    {
        "error": {
            "fields": {
                "contact_fields": {
                    "message": "Provided contact fields do not contain required values",
                    "code": "bad_contact_field_value"
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }

```