# SurveyRespondentsExport

> Оригинал: [https://ads.vk.com/doc/api/resource/SurveyRespondentsExport](https://ads.vk.com/doc/api/resource/SurveyRespondentsExport)

---

## /api/v1/lead_ads/survey_forms//respondents.xlsx

Ресурс, позволяющий получить собранные данные респондентов, прошедших опрос. На текущий момент доступен экспорт только в формате xlsx-файла.

### GET

Пример запроса

```HTTP

    GET /api/v1/lead_ads/survey_forms/17/respondents.xlsx
```

Фильтры

- _created_at - Дата и время получения ответа респондента. Доступные ограничения "lte" - меньше или равно, "gte" - больше или равно

```HTTP

    /api/v1/lead_ads/survey_forms/17/respondents.xlsx?_created_at__lte=2022-01-01%2000:00:00
    /api/v1/lead_ads/survey_forms/17/respondents.xlsx?_created_at__gte=2022-01-01%2000:00:00
```

- _ad_plan_id - ID рекламных кампаний

```HTTP

    /api/v1/lead_ads/survey_forms/17/respondents.xlsx?_ad_plan_id__in=6617841,6711647
```

- _ad_group_id - ID рекламных групп

```HTTP

    /api/v1/lead_ads/survey_forms/17/respondents.xlsx?_ad_group_id__in=6617841,6711647
```

- _banner_id - ID рекламных объявлений

```HTTP

    /api/v1/lead_ads/survey_forms/17/respondents.xlsx?_banner_id__in=6617841,6711647
```

Возможные коды ответа

- 200 - объявление сохранено
- 404 - опрос не найденda:T717,Объект, описывающий элемент списка респондентов с опросов. Представляет собой развернутую информацию о респонденте.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|string|`readable`|Идентификатор респондента|
|survey_id|string|`readable`|Идентификатор опроса|
|survey_name|string|`readable` |Название опрос