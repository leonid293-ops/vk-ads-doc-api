# SurveysListElement

> Оригинал: [https://ads.vk.com/doc/api/object/SurveysListElement](https://ads.vk.com/doc/api/object/SurveysListElement)

---

Объект, описывающий элемент списка опросов. Представляет собой сокращенную информацию об опросе.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|string|`readable`|Идентификатор опроса|
|name|string|`readable`|Название опроса|
|url|string|`readable`|Прямая ссылка на опрос|
|status|integer|`readable``writable` `choices =`
  - `1` - Активная 
  - `2` - В архиве|Статус опроса. Перевод активного опроса в архив и обратно выполняется только специльными запросами. Для опросов в архиве недоступно обновление|
|created|datetime|`readable`|Время создания|
|updated|datetime|`readable`|Время последнего обновления|
|respondents_count|integer|`readable`|Количество респондентов, собранных опросом|
|ad_plans_count|integer|`readable`|Количество рекламных кампаний, в которых используется опрос|
|ad_plan_ids|list of uint32|`readable`|Идентификаторы рекламных кампаний, в которых используется опрос|
|ad_group_ids|list of uint32|`readable`|Идентификаторы рекламных групп, в которых используется опрос|
|banner_ids|list of uint32|`readable`|Идентификаторы рекламных объявлений, в которых используется опрос|
|active_ad_plan_ids|list of uint32|`readable`|Идентификаторы активных рекламных кампаний, в которых используется опрос|
|logo|object|`readable`|Логотип компании|