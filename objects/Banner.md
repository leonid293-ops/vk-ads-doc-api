# Banner

> Оригинал: [https://ads.vk.com/doc/api/object/Banner](https://ads.vk.com/doc/api/object/Banner)

---

Объект, описывающий рекламное объявление кампании.

Используется в методах: [Banners](../resource/Banners), [Banner](../resource/Banner)

Используется в объектах: [AdGroup](../object/AdGroup)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|uint32|`readable` `default_field`|Идентификатор объявления|
|created|datetime|`readable`|Время создания|
|updated|datetime|`readable`|Время последнего обновления|
|name|string|`readable` `writable`|Название баннера|
|status|string|`readable` `writable` `choices =`
  - `active` - Активный 
  - `deleted` - Удаленный 
  - `blocked` - Заблокированный|Статус объявления. Также может возвращаться статус deleted для удаленных баннеров. В объявлении со статусом deleted возможно только изменение статуса|
|ad_group_id|uint32|`readable` `default_field`|Идентификатор рекламной группы|
|content|object with [BannerContent](../object/BannerContent) as values|`readable` `writable`|Содержимое баннера. Должно соответствовать структуре content [баннерному полю](../object/BannerField) пакета рекламной группы.|
|delivery|string|`readable`|Статус трансляции баннера. Возможные значения: pending - баннер ожидает модерации; delivering - баннер может показываться; not_delivering - баннер не может показываться, причины описаны в поле issues|
|issues|list of object|`readable`|Описание причин непоказа объявления:
  - `ACCOUNT_INACTIVE` - Account is inactive.
  - `BANNER_STOPPED` - The banner is stopped.
  - `BANNER_ARCHIVED` - The banner is removed.
  - `CAMPAIGN_STOPPED` - The campaign is stopped.
  - `CAMPAIGN_ARCHIVED` - The campaign is removed.
  - `BANNER_BANNED` - The banner is rejected by moderation.
  - `BANNER_ON_MODERATION` - The banner is on moderation.|
|moderation_reasons|list of [ModerationReason](../object/ModerationReason)|`readable`|Причины, по которым объявление было запрещено|
|moderation_status|string|`readable` `default_field`|Статус модерации объявления. Возможные значения: pending - объявление не промодерировано; allowed - объявление разрешено; banned - объявление запрещено|
|textblocks|object with [Textblock](../object/Textblock) as values|`readable` `writable`|Блоки текстового содержимого. Должно соответствовать структуре textblocks [баннерного поля](../object/BannerField) пакета рекламной группы.|
|urls|object with [Urls](../object/Urls) as values|`readable` `writable`|Объекты ссылок. Должно соответствовать структуре urls [баннерного поля](../object/BannerField) пакета рекламной группы.|
|ord_marker|string|`readable``max_length=32``default_field`|Токен маркировки креатива|