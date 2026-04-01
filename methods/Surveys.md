# Surveys

> Оригинал: [https://ads.vk.com/doc/api/resource/Surveys](https://ads.vk.com/doc/api/resource/Surveys)

---

## /api/v1/lead_ads/survey_forms.json

Ресурс, позволяющий создать новый опрос или получить список существующих опросов

### GET

Получение списка опросов

Пример запроса

```HTTP

    GET /api/v1/lead_ads/survey_forms.json
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
                "name": "New survey 2022-07-15 17:53"
                ...
            },
            {
                "id": 105,
                "name": "New survey 2022-08-16 19:49"
                ...
            },
            {
                "id": 42303,
                "name": "New survey 2022-08-16 19:51"
                ...
            }
        ]
    }
```

Доступные поля - описаны в [SurveysListElement](../object/SurveysListElement)

Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

- limit - количество опросов в ответе. По умолчанию 20. Максимум 50

```HTTP

    /api/v1/lead_ads/survey_forms.json?limit=10
```

- offset - смещение на N опросов от начала текущей выборки

```HTTP

    /api/v1/lead_ads/survey_forms.json?limit=5&offset=15
```

Фильтры

- _ad_plan_ids - ID рекламных кампаний

```HTTP

    /api/v1/lead_ads/survey_forms.json?_ad_plan_ids__in=6617841,6711647
```

- _ad_group_ids - ID рекламных групп

```HTTP

    /api/v1/lead_ads/survey_forms.json?_ad_group_ids__in=6617841,6711647
```

- _banner_ids - ID рекламных объявлений

```HTTP

    /api/v1/lead_ads/survey_forms.json?_banner_ids__in=6617841,6711647
```

- q - cтрока для поиска по опросам. Поиск происходит по имени опроса, учитываются полные вхождения слов

```HTTP

    /api/v1/lead_ads/survey_forms.json?q=new
```

Сортировка

- id

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=id - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-id - по убыванию
```

- name

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=name - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-name - по убыванию
```

- status

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=status - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-status - по убыванию
```

- created

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=created - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-created - по убыванию
```

- updated

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=updated - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-updated - по убыванию
```

- respondents_count

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=respondents_count - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-respondents_count - по убыванию
```

- ad_plans_count

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting= ad_plans_count - по возрастанию
    /api/v1/lead_ads/survey_forms.json?sorting=-ad_plans_count - по убыванию
```

- по нескольким полям

```HTTP

    /api/v1/lead_ads/survey_forms.json?sorting=status,name,-id

```

Дополнительные флаги

- get_active_form_ad_plans - флаг, указывающий, нужно ли возвращать id активных ad_plan'ов для опросов. Если не указан, то по умолчанию они не возвращаются

```HTTP

    /api/v1/lead_ads/survey_forms.json?get_active_form_ad_plans=1
```

### POST

Создание опроса. Структура передаваемого объекта опроса описана в [Survey](../object/Survey).

Пример запроса:

```HTTP

    POST /api/v1/lead_ads/survey_forms.json
    {
    "name": "Опрос из Кремниевой долины",
    "first_screen_type": "text",
    "title": "Кто вы в «Кремниевой долине»?",
    "description": "Следуй за нами в будущее!",
    "company_title": "Пегий Дудочник",
    "result_info": {
        "positive": {
            "title": "Спасибо, а теперь",
            "description": "Следуйте за нами в будущее",
            "site_url": "http://piedpiper.com.ru/index.html?utm_source=pied_piper&utm_medium=hooli",
            "cta_text": "Перейти на сайт"
        }
    },
    "pages": [
        {
            "blocks": [
                {
                    "block_data": {
                        "type": "question",
                        "data": {
                            "is_required": true,
                            "text": "Как выйти из Vim?",
                            "type": "multiple_answers",
                            "answers": [
                                {
                                    "type": 0,
                                    "text": "Ctrl + Alt + Del -> Enter"
                                },
                                {
                                    "type": 0,
                                    "text": "Выключить свет и выйти"
                                },
                                {
                                    "type": 0,
                                    "text": "Esc -> :wq"
                                },
                                {
                                    "type": 0,
                                    "text": "Ctrl + D"
                                },
                                {
                                    "type": 0,
                                    "text": "Ctrl + X"
                                },
                                {
                                    "type": 2,
                                    "text": ""
                                }
                            ]
                        }
                    }
                }
            ]
        },
        {
            "blocks": [
                {
                    "block_data": {
                        "type": "question",
                        "data": {
                            "is_required": true,
                            "type": "one_answer",
                            "answers": [
                                {
                                    "type": 0,
                                    "text": "Табы для питонистов"
                                },
                                {
                                    "type": 0,
                                    "text": "Как скажет тимлид, таков путь"
                                },
                                {
                                    "type": 4,
                                    "text": ""
                                }
                            ]
                        }
                    }
                }
            ]
        }
    ],
    "logo_id": "4242eafb-4242-4242-4242-424ec4de4242",
    "gradient": 3
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

При создании опроса ему устанавливается статус active.

Возможные коды ответа

- 200 - опрос сохранен
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