# Segment

> Оригинал: [https://ads.vk.com/doc/api/object/Segment](https://ads.vk.com/doc/api/object/Segment)

---

Сегмент аудитории.

Используется в методах: [Segments](../resource/Segments), [Segment](../resource/Segment)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|campaign_ids|list of integer|`readable` `min_value=-2147483647` `max_value=2147483647`|Идентификаторы кампаний, таргетированных на сегмент|
|created|datetime|`readable` `default_field`|Дата и время создания|
|flags|list of string|`readable` `default_field`|Флаги. "sharing_forbidden" - сегментом запрещено делиться с другими пользователями, т.к. он содержит сторонние источники данных или сегменты|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор сегмента|
|name|string|`readable` `required` `writable` `default_field`|Название сегмента|
|pass_condition|integer|`readable` `required` `writable` `default_field` `max_value=2147483647`|Условие включения пользователя в сегмент в зависимости от количества источников данных сегмента, в которые он входит. Минимальное значение: "1" – пользователь должен быть минимум в одном источнике. Максимальное значение: "relations count" – пользователь должен быть во всех источниках сегмента|
|relations|list of [SegmentRelation](../object/SegmentRelation)|`readable` `required` `writable` `create_only`|Источники данных в сегменте|
|relations_count|integer|`readable` `max_value=2147483647`|Количество источников данных в сегменте|
|updated|datetime|`readable` `default_field`|Дата и время обновления|
|users|list of [SegmentUser](../object/SegmentUser)|`readable`|Пользователи, обладающие доступом к сегменту|