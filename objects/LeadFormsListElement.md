# LeadFormsListElement

> Оригинал: [https://ads.vk.com/doc/api/object/LeadFormsListElement](https://ads.vk.com/doc/api/object/LeadFormsListElement)

---

Объект, описывающий элемент списка лид форм. Представляет собой сокращенную информацию о лид форме.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|string|`readable`|Идентификатор формы|
|name|string|`readable`|Название формы|
|status|integer|`readable``writable` `choices =`
  - `1` - Активная 
  - `2` - В архиве|Статус формы. Перевод активной формы в архив и обратно выполняется только специльными запросами. Для форм в архиве недоступно обновление|
|created|datetime|`readable`|Время создания|
|updated|datetime|`readable`|Время последнего обновления|
|leads_count|integer|`readable`|Количество лидов, собранных формой|
|ad_plans_count|integer|`readable`|Количество рекламных кампаний, в которых используется форма|
|ad_plan_ids|list of uint32|`readable`|Идентификаторы рекламных кампаний, в которых используется форма|
|ad_group_ids|list of uint32|`readable`|Идентификаторы рекламных групп, в которых используется форма|
|banner_ids|list of uint32|`readable`|Идентификаторы рекламных объявлений, в которых используется форма|
|active_ad_plan_ids|list of uint32|`readable`|Идентификаторы активных рекламных кампаний, в которых используется форма|
|notification_actions|list of string|`readable``choices =`
  - `email` - Почта 
  - `vk` - VK мессенджер|Список мест, куда настроены уведомления о событиях формы|
|logo|object|`readable`|Логотип компании|
|main_image|object|`readable`|Обложка формы|