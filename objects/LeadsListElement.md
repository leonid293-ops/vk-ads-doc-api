# LeadsListElement

> Оригинал: [https://ads.vk.com/doc/api/object/LeadsListElement](https://ads.vk.com/doc/api/object/LeadsListElement)

---

Объект, описывающий элемент списка лидов с лид форм. Представляет собой развернутую информацию о лиде.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|string|`readable`|Идентификатор лида|
|form_id|string|`readable`|Идентификатор формы|
|form_name|string|`readable` |Название формы|
|ad_plan_id|uint32|`readable`|Идентификатор рекламной кампании, с которой был получен лид|
|ad_group_id|uint32|`readable`|Идентификатор рекламной группы, с которой был получен лид|
|banner_id|uint32|`readable`|Идентификатор рекламного объявления, с которого был получен лид|
|created_at|datetime|`readable`|Время получение лида|
|contact_info|[ContactInfo](../object/LeadContactInfo)|`readable`|Контактные данные лида|
|answers|list of [LeadAnswer](../object/LeadAnswer)|`readable`|Ответы лида на вопросы формы|cc:Te3e,