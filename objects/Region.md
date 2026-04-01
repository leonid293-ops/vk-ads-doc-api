# Region

> Оригинал: [https://ads.vk.com/doc/api/object/Region](https://ads.vk.com/doc/api/object/Region)

---

Объект, содержащий информацию о регионе.

Используется в методах: [Region](../resource/Region)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|flags|list of string|`readable` `default_field`|Флаги, отображающие принадлежность региона к тому или иному геодереву. Пример находится в связанном [методе](../resource/Region)|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор региона|
|iso_alpha_3|string|`readable`|Код страны в формате ISO 3166-1 alpha-3|
|name|string|`readable` `default_field`|Название региона|
|parent_id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор родительского региона|
|type|string|`readable`|Тип региона|6c:T82c,