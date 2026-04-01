# BannerMassReplace

> Оригинал: [https://ads.vk.com/doc/api/object/BannerMassReplace](https://ads.vk.com/doc/api/object/BannerMassReplace)

---

Объект, позволяющий массово изменять текст и ссылки баннеров.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|change_from|string|`readable` `required` `writable`|Текст, который будет найден и заменен.|
|change_to|string|`readable` `required` `writable`|Новый текст, который будет использован после замены.|
|field|string|`readable` `required` `writable` `choices =`
  - `urls` - ссылки 
  - `textblocks` - текстблоки|Поле, в котором будет совершена замена.|
|ids|list of id|`readable` `required` `writable` `min_value=1` `max_value=2147483647`|Идентификаторы баннеров.|5c:T4e6,Объект, описывающий цель счетчика [Top@Mail.ru](https://top.mail.ru)

Используется в объектах: [Goals](../object/Goals)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|counter_id|integer|`readable` `default_field` `min_value=-2147483647` `max_value=2147483647`|Идентификатор счетчика в [Top@Mail.ru](https://top.mail.ru)|
|counter_name|string|`readable` `default_field`|Н