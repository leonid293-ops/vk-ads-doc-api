# AdGroupMassAction

> Оригинал: [https://ads.vk.com/doc/api/object/AdGroupMassAction](https://ads.vk.com/doc/api/object/AdGroupMassAction)

---

Объект, содержащий изменения данных группы

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|int32|`readable` `required` `writable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор рекламной группы|
|status|string|`readable` `writable` `default_field` `choices =`
  - `active` - Активная 
  - `deleted` - Удаленная 
  - `blocked` - Заблокированная|Статус рекламной группы|
|targetings|[TargetingsMassAction](../object/TargetingsMassAction)|`readable` `writable`|Структура таргетингов|
|budget_limit|decimal|`readable` `writable`|Общий бюджет рекламной группы|
|budget_limit_day|decimal|`readable` `writable`|Бюджет рекламной группы на день|
|date_start|date|`readable` `writable`|Дата старта
|date_end|date|`readable` `writable`|Дата окончания
|max_price|decimal|`readable` `writable`|Предельная цена конверсииbb:T109c,