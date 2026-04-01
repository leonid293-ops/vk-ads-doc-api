# IconImage

> Оригинал: [https://ads.vk.com/doc/api/object/IconImage](https://ads.vk.com/doc/api/object/IconImage)

---

Объект, содержащий информацию о картинке баннера мобильного приложения.

Используется в объектах: [GoogleApp](../object/GoogleApp), [AppleApp](../object/AppleApp)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|height|integer|`readable` `required` `default_field` `min_value=-2147483647` `max_value=2147483647`|Высота в пикселях|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Внутрений идентификатор изображения VK Ads|
|preview_url|string|`readable` `required` `default_field`|Урл изображения|
|size|integer|`readable` `required` `default_field` `min_value=-2147483647` `max_value=2147483647`|Размер в байтах|
|width|integer|`readable` `required` `default_field` `min_value=-2147483647` `max_value=2147483647`|Ширина в пикселях|63:T60b,Объект, описывающий событие в мобильном приложении.

Используется в методах: [InAppEvent](../resource/InAppEvent)

Используется в объектах: [InAppTracker](../object/InAppTracker)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|count|[RemarketingInAppEventCount](../obje