# LeadFormLeadsExport

> Оригинал: [https://ads.vk.com/doc/api/resource/LeadFormLeadsExport](https://ads.vk.com/doc/api/resource/LeadFormLeadsExport)

---

## /api/v1/lead_ads/lead_forms//leads.

Ресурс, позволяющий получить собранные данные лидов, заполнивших форму. На текущий момент доступны следующие форматы для экспорта:
- csv
- xlsx

### GET

Пример запроса

```HTTP

    GET /api/v1/lead_ads/lead_forms/17/leads.csv
```

Пример ответа

```HTTP

    HTTP 200
    "ID Кампании","ID Группы","ID Объявления","Время лида","Имя","Телефон","Есть ли у вас домашнее животное?"
    "1","3","2","2022-12-08 21:41:03.922 +0000 UTC","Виктор","+78008005555","Да"
```

Фильтры

- _created_at - Дата и время получения лида. Доступные ограничения "lte" - меньше или равно, "gte" - больше или равно

```HTTP

    /api/v1/lead_ads/lead_forms/17/leads.csv?_created_at__lte=2022-01-01%2000:00:00
    /api/v1/lead_ads/lead_forms/17/leads.csv?_created_at__gte=2022-01-01%2000:00:00
```

- _ad_plan_id - ID рекламных кампаний

```HTTP

    /api/v1/lead_ads/lead_forms/17/leads.csv?_ad_plan_id__in=6617841,6711647
```

- _ad_group_id - ID рекламных групп

```HTTP

    /api/v1/lead_ads/lead_forms/17/leads.csv?_ad_group_id__in=6617841,6711647
```

- _banner_id - ID рекламных объявлений

```HTTP

    /api/v1/lead_ads/lead_forms/17/leads.csv?_banner_id__in=6617841,6711647
```

Возможные коды ответа

- 200 - объявление сохранено
- 404 - лид форма не найденаc8:T6d0,## /api/v1/lead_ads/upload_image/

Ресурс, позволяющий загрузить изображение для его последующего использования в лид форме. На текущий момент доступны следующие роли для изображени