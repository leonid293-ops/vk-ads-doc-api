# Survey

> Оригинал: [https://ads.vk.com/doc/api/resource/Survey](https://ads.vk.com/doc/api/resource/Survey)

---

## /api/v1/lead_ads/survey_forms/.json

Ресурс, позволяющий получать и обновлять опросы.

### GET

Получение одного опроса

Пример запроса

```HTTP

    GET /api/v1/lead_ads/survey_forms/17.json
```

Пример ответа

```HTTP

    {
        "id": "17",
        "name": "Мой первый опрос"
    }

```

Доступные поля - описаны в [Survey](../object/Survey)

Параметры

- get_active_form_ad_plans - флаг, указывающий, нужно ли возвращать id активных ad_plan'ов для опроса. Если не указан, то по умолчанию они не возвращаются

```HTTP

    /api/v1/lead_ads/survey_forms/17.json?get_active_form_ad_plans=1
```

### POST

Редактирование опроса. Доступные поля описаны в [Survey](../object/Survey).

Пример запроса

```HTTP

    POST /api/v1/lead_ads/survey_forms/17.json
    {
        "name": "VK реклама. Обновленный опрос"
    }
```

Пример ответа

```HTTP

    HTTP 200
    {
        "id": "17",
        "name": "VK реклама. Обновленный опрос",
        ...
    }
```

Содержимое секций result_info и pages полностью замещается при обновлении.

Возможные коды ответа

- 200 - объявление сохранено
- 400 - ошибка валидации
- 404 - опрос не найден

Возможные коды ошибок

- bad_value - неправильный формат или тип значения
- required - поле обязательно
- required_value - ожидается обязательное значение
- unallowed_value - значение не входит в список достимых
- bad_items - в списке присутствуют неправильные значения
- max_value - длина/размер строки/списка больше максимального
- min_value - длина/размер строки/списка меньше минимального
- duplicate_value - в списке встречаются повторяющиеся значения

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
                "field": {
                    "message": "Bad items",
                    "code": "bad_items"
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }

```