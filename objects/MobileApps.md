# MobileApps

> Оригинал: [https://ads.vk.com/doc/api/object/MobileApps](https://ads.vk.com/doc/api/object/MobileApps)

---

Объект, описывающий доступное пользователю мобильное приложение вместе со списком пользователей, которые имеют к нему доступ.

Используется в методах: [MobileApps](../resource/MobileApps)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|app_name|string|`readable` `default_field`|Название мобильного приложения|
|campaign_ids|list of integer|`readable`  `max_value=2147483647`|Массив ID кампаний, связанных с этим мобильным приложением|
|platform|string|`readable` `default_field`|Обозначение платформы мобильного приложения|
|preview_url|url|`readable`|URL превью-изображения|
|rb_mobile_app_id|integer|`readable` `default_field` `max_value=2147483647`|Внутренний ID мобильного приложения|
|category_id|integer|`readable` `max_value=2147483647`|Внутренний ID категории мобильного приложения|
|sk_ad_network_ids|[SkAdNetworkIdsCounts](../object/SkAdNetworkIdsCounts)|`readable`|Объект с информацией о доступных и используемых идентификаторах кампании `SkAd Network`|
|url|string|`readable`|URL приложения|
|url_object_id|string|`readable` `default_field`|Внутренний идентификатор URL приложения|
|users|list of objects|`readable`|Пользователи, имеющие доступ к мобильному приложению|