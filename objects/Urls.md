# Urls

> Оригинал: [https://ads.vk.com/doc/api/object/Urls](https://ads.vk.com/doc/api/object/Urls)

---

Объект, описывающий ссылки объявления.

Используется в объектах: [Banner](../object/Banner), [BannerMassAction](../object/BannerMassAction)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|id|`readable` `required` `writable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор ссылки|
|url|url|`readable`|Ссылка|
|url_object_id|string|`readable`|Идентификатор связанного объекта|
|url_object_type|string|`readable`|Тип связанного объекта|
|url_types|list of string|`readable`|Типы ссылки, которые были определены автоматически. Для использования в рекламных объявлениях ссылка должна содержать тип, указанный в [баннерном формате](../object/BannerFormat) в поле "fields"|78:T640,Объект, хранящий информацию о клиенте и ссылки на связанные объекты.

Используется в объектах: [AgencyClient](../object/AgencyClient)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|uin32|`readable` `writable` `default_field`|Идентификатор клиента|
|status|string|`readable` `choices =`
  - `active` - Активный 
  - `deleted` - Удаленный 
  - <span cl