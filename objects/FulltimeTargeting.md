# FulltimeTargeting

> Оригинал: [https://ads.vk.com/doc/api/object/FulltimeTargeting](https://ads.vk.com/doc/api/object/FulltimeTargeting)

---

Время показа кампании.

Используется в объектах: [Targetings](../object/Targetings)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|flags|list of string|`readable` `writable`|use_holidays_moving - Учитывать перенос праздничных дней cross_timezone - Учитывать временные зоны|
|fri|list of integer|`readable` `writable` `max_value=23`|Часы в пятницу|
|mon|list of integer|`readable` `writable` `max_value=23`|Часы в понедельник|
|sat|list of integer|`readable` `writable` `max_value=23`|Часы в субботу|
|sun|list of integer|`readable` `writable` `max_value=23`|Часы в воскресенье|
|thu|list of integer|`readable` `writable` `max_value=23`|Часы в четверг|
|tue|list of integer|`readable` `writable` `max_value=23`|Часы во вторник|
|wed|list of integer|`readable` `writable` `max_value=23`|Часы в среду|60:T52a,Объект, содержащий описания целей конверсий, разбитые по типам. Содержит только типы, доступные в кампаниях пользователя.

Используется в