# SegmentRelation

> Оригинал: [https://ads.vk.com/doc/api/object/SegmentRelation](https://ads.vk.com/doc/api/object/SegmentRelation)

---

Связь сегмента с включенным в него источником данных или вложенным сегментом.

Используется в методах: [SegmentRelations](../resource/SegmentRelations), [SegmentRelationsDelete](../resource/SegmentRelationsDelete), [SegmentRelation](../resource/SegmentRelation)

Используется в объектах: [Segment](../object/Segment)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор связи|
|object_id|integer|`readable` `writable` `default_field` `create_only` `min_value=-2147483647` `max_value=2147483647`|Идентификатор объекта|
|object_type|string|`readable` `required` `writable` `default_field` `create_only` `choices =`
  - `remarketing_player` - Пользователи, использовавшие приложения на платформе 
  - `interest_categories` - Интересы 
  - `remarketing_vk_app` - Пользователи приложения ВКонтакте 
  - `remarketing_inapp_event` - События в приложении 
  - `remarketing_search_phrases` - Список поисковых фраз 
  - `remarketing_campaign_list` - Список кампаний 
  - `remarketing_local_geo` - Локальная география 
  - `interest_visits` - Интересы 
  - `remarketing_game_player` - Пользователи приложения Одноклассники 
  - `remarketing_mobile_app` - Пользователи мобильного приложения 
  - `remarketing_vk_group` - Пользователи, вступившие в группу в ВКонтакте 
  - `interest` - Интересы 
  - `remarketing_group` - Пользователи, вступившие в группу на Одноклассниках 
  - `remarketing_users_list` - Список пользовательских идентификаторов 
  - `remarketing_user_geo` - Пользовательская география 
  - `remarketing_pricelist` - Прайс-лист динамического ремаркетинга 
  - `remarketing_lookalike_audience` - Lookalike-аудитория. 
  - `segment` - Вложенный сегмент 
  - `remarketing_game_payer` - Пользователи, платившие за приложение Одноклассники 
  - `remarketing_app_category` - Категория приложений Android 
  - `age` - Возраст 
  - `remarketing_counter` - Счетчик [Top@Mail.ru](https://top.mail.ru) 
  - `remarketing_custom_audience` - Типовая аудитория 
  - `remarketing_payer` - Платившие на платформе|Тип вложенного объекта|
|params|object|`readable` `writable`|Параметры источника данных. Описание параметров для разных типов источников можно посмотреть [здесь](../info/SegmentParams)|