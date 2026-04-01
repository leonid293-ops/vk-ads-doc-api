# SharingKeySource

> Оригинал: [https://ads.vk.com/doc/api/object/SharingKeySource](https://ads.vk.com/doc/api/object/SharingKeySource)

---

Источник данных, содержащийся в ключе.

Используется в объектах: [SharingKey](../object/SharingKey)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|key|string|`readable`|Ключ|
|object_id|integer|`readable` `required` `writable` `default_field` `min_value=-2147483647` `max_value=2147483647`|Идентификатор источника|
|object_type|string|`readable` `required` `writable` `default_field` `choices =`
  - `users_list` - Список пользователей 
  - `counter` - Счетчик [Top@Mail.ru](https://top.mail.ru)  
  - `campaign_list` - Рекламные кампании 
  - `custom_audience` - Типовые аудитории  
  - `pricelist` - Продуктовый фид  
  - `segment` - Сегмент 
  - `lookalike_audience` - Look-Alike аудитория|Тип источника|72:T4b8,Объект, используемый при активации ключа пользователем.

Используется в методах: [SharingKeyUser](../resource/SharingKeyUser)

Используется в объектах: [SharingKey](../object/SharingKey)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|id|`readable` `default_field` <span class="