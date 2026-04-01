# LeadForms

> Оригинал: [https://ads.vk.com/doc/api/resource/LeadForms](https://ads.vk.com/doc/api/resource/LeadForms)

---

## /api/v1/lead_ads/lead_forms.json

Ресурс, позволяющий создать новую или получить список существующих лид форм

### GET

Получение списка лид форм

Пример запроса

```HTTP

    GET /api/v1/lead_ads/lead_forms.json
```

Пример ответа

```HTTP

    {
        "count": 3,
        "offset": 0,
        "limit": 5,
        "items": [
            {
                "id": 2523,
                "name": "New lead form 2022-07-15 17:53"
                ...
            },
            {
                "id": 105,
                "name": "New lead form 2022-08-16 19:49"
                ...
            },
            {
                "id": 42303,
                "name": "New lead form 2022-08-16 19:51"
                ...
            }
        ]
    }
```

Доступные поля - описаны в [LeadFormsListElement](../object/LeadFormsListElement)

Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

- limit - количество форм в ответе. По умолчанию 20. Максимум 50

```HTTP

    /api/v1/lead_ads/lead_forms.json?limit=10
```

- offset - смещение на N форм от начала текущей выборки

```HTTP

    /api/v1/lead_ads/lead_forms.json?limit=5&offset=15
```

Фильтры

- _ad_plan_ids - ID рекламных кампаний

```HTTP

    /api/v1/lead_ads/lead_forms.json?_ad_plan_ids__in=6617841,6711647
```

- _ad_group_ids - ID рекламных групп

```HTTP

    /api/v1/lead_ads/lead_forms.json?_ad_group_ids__in=6617841,6711647
```

- _banner_ids - ID рекламных объявлений

```HTTP

    /api/v1/lead_ads/lead_forms.json?_banner_ids__in=6617841,6711647
```

- q - cтрока для поиска по формам. Поиск происходит по имени формы, учитываются полные вхождения слов

```HTTP

    /api/v1/lead_ads/lead_forms.json?q=new
```

Сортировка

- id

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=id - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-id - по убыванию
```

- name

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=name - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-name - по убыванию
```

- status

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=status - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-status - по убыванию
```

- created

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=created - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-created - по убыванию
```

- updated

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=updated - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-updated - по убыванию
```

- leads_count

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=leads_count - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-leads_count - по убыванию
```

- ad_plans_count

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting= ad_plans_count - по возрастанию
    /api/v1/lead_ads/lead_forms.json?sorting=-ad_plans_count - по убыванию
```

- по нескольким полям

```HTTP

    /api/v1/lead_ads/lead_forms.json?sorting=status,name,-id

```

Дополнительные флаги

- get_active_form_ad_plans - флаг, указывающий, нужно ли возвращать id активных ad_plan'ов для форм. Если не указан, то по умолчанию они не возвращаются

```HTTP

    /api/v1/lead_ads/lead_forms.json?get_active_form_ad_plans=1
```

### POST

Создание лид формы

Пример запроса:

```HTTP

    POST /api/v1/lead_ads/lead_forms.json
    {
        "name": "Моя первая лидформа",
        "company_title": "ВКонтакте",
        "logo_id": "96a871b5-04c7-45b0-9a8d-565f65bd14c5",
        "contact_fields": [
            "first_name",
            "phone"
        ],
        "result_info": {
            "title": "Спасибо!",
            "description": "Ваша заявка успешно отправлена!",
            "site_url": "https://mail.ru",
            "phone": "+78008005555"
        },
        "agreement": {
            "usage": "template_document",
            "template_document": {
                  "company_title": "VK",
                  "registration_address": "Ленинградский проспект, 39"
            }
        }
    }
```

Пример ответа:

```HTTP

    HTTP 200
    {
        "id": 9826424
        ...
    }
```

При создании формы ей устанавливается статус active.

Возможные коды ответа

- 200 - форма сохранена
- 400 - ошибка валидации

Возможные коды ошибок:
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

где field_name_N - название поля, в котором произошла ошибка, error_message_N - описание ошибки, error_code_N - код ошибки.

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