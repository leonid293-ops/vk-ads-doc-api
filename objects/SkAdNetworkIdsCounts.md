# SkAdNetworkIdsCounts

> Оригинал: [https://ads.vk.com/doc/api/object/SkAdNetworkIdsCounts](https://ads.vk.com/doc/api/object/SkAdNetworkIdsCounts)

---

Этот объект описывает количество собственных и выданных агентам идентификаторов кампании SkAd Network. Используется в ресурсе [MobileApps](../resource/MobileApps) в составе объекта [MobileApps](../object/MobileApps).

Используется в объектах: [MobileApps](../object/MobileApps)

|Field name|Type|Conditions|Description|
|-|-|-|-|
| available |integer|`readable` `default_field` `min_value=0` `max_value=100`| Количество идентификаторов кампании SkAd Network, которые принадлежат пользователю и не использованы в рекламных кампаниях|
| inherited_available |integer|`readable` `default_field` `min_value=0` `max_value=100`|Количество идентификаторов кампании SkAd Network, которые были выданы агентам, но не были использованы ими в рекламных кампаниях|
| inherited_total |integer|`readable` `default_field` `min_value=0` `max_value=100`|Количество идентификаторов кампании SkAd Network, которые были выданы агентам (включая те, что были использованы ими в рекламных кампаниях)|
| inherited_used |integer|`readable` `default_field` `min_value=0` `max_value=100`|Количество идентификаторов кампании SkAd Network, которые были выданы агентам и использованы ими в рекламных кампаниях|
| total |integer|`readable` `default_field` `min_value=0` `max_value=100`|Количество идентификаторов кампании SkAd Network, принадлежащих пользователю (включая использованные в кампаниях, но без тех, что были выданы агентам)|
| used |integer|`readable` `default_field` `min_value=0` `max_value=100`|Количество идентификаторов кампании SkAd Network, которые заняты кампаниями пользователя|