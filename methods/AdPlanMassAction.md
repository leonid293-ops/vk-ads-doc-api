# AdPlanMassAction

> Оригинал: [https://ads.vk.com/doc/api/resource/AdPlanMassAction](https://ads.vk.com/doc/api/resource/AdPlanMassAction)

---

## /api/v2/ad_plans/mass_action.json

Ресурс, позволяющий массово обновлять данные кампаний (не более 200 кампаний за раз).

Используется объект: [AdPlanMassAction](../object/AdPlanMassAction)

### POST

В теле запроса указывается структура вида: 

```HTTP
[
  {
    "id": 2147483647,
    "status": "active",
    "budget_limit_day": 10000,
    "date_start": "2022-11-27",
    "date_end": "2022-11-27",
    "max_price": 21474836.47
  }
]
```

Пример запроса:

```HTTP
POST /api/v2/ad_plans/mass_action.json
[
  {
    "id": 123456,
    "status": "active",
    "max_price": 200
  },
  {
    "id": 234567,
    "status": "blocked"
  }
]
```

В случае успеха, ответ будет иметь статус 204.

Возможные ошибки: 

1) Превышение лимита количества кампаний в запросе: 

```HTTP
{
  "error": {
    "message": "Too much items. Limit is 200",
    "code": "limit_exceeded"
  }
}
```

2) В запросе указаны несуществующие кампании: 

```HTTP
{
  "error": {
    "message": "Unknown ad_plans: 144, 42, 100500",
    "code": "unknown_ad_plans"
  }
}
```bd:T70a,Объект, содержащий изменения данных кампаний

Используется в методах: [AdPlanMassAction](../resource/AdPlanMassAction)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|int32|`readable` `required` `writable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор кампании|
|status|string|`readable` `writable` `default_field` <s