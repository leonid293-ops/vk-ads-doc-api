# PackagePad

> Оригинал: [https://ads.vk.com/doc/api/object/PackagePad](https://ads.vk.com/doc/api/object/PackagePad)

---

Описание площадок, которые используются в таргетингах пакета по умолчанию.

Используется в методах: [PackagesPads](../resource/PackagesPads)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|description|string|`readable` `default_field`|Описание площадки|
|eye_url|object|`readable` `default_field`|URL места размещения объявления. Возможные ключи: "id", "description", "url"|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор площадки|
|name|string|`readable` `default_field`|Имя площадки|
|patterns|string|`readable` `default_field`|Поддерживаемые площадкой паттерны баннеров|6a:T2054,