# Targetings

> Оригинал: [https://ads.vk.com/doc/api/object/Targetings](https://ads.vk.com/doc/api/object/Targetings)

---

Таргетинги. Доступные таргетинги описаны в [объекте пакета](../object/Package), в рамках которого создаётся кампания.

Используется в объектах: [AdGroup](../object/AdGroup)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|age|[AgeTargeting](../object/AgeTargeting)|`readable` `writable`|Возраст (список возрастов). 0 - показывать тем, чей возраст не определён|
|birthday|[BirthdayTargeting](../object/BirthdayTargeting)|`readable` `writable`|День рождения|
|fulltime|[FulltimeTargeting](../object/FulltimeTargeting)|`readable` `writable`|Время (дни и часы)|
|geo|[GeoTargeting](../object/GeoTargeting)|`readable` `writable`|Общий таргетинг географии, объединяющий [геолокации](../object/LocalGeoTargeting) и регионы (список идентификаторов регионов). Возможна установка только одного из значений - local_geo или regions. [Список доступных регионов](../resource/Region)|
|group_members|string|`readable` `writable` `choices =`
  - `all` - Все 
  - `group_member` - В группе 
  - `not_group_member` - Не в группе|Вхождение в группу ОК/VK|
|interests|list of integer|`readable` `writable` `max_value=2147483647`|Интересы пользователей. [Список доступных интересов](../resource/TargetingsTree)|
|interests_soc_dem|list of integer|`readable` `writable` `max_value=2147483647`|Социально-демографические интересы пользователей. [Список доступных интересов](../resource/TargetingsTree)|
|interests_stable|list of integer|`readable` `writable` `max_value=2147483647`|Долгосрочные интересы пользователей. [Список доступных интересов](../resource/TargetingsTree)|
|local_geo|[LocalGeoTargeting](../object/LocalGeoTargeting)|`readable` `writable`|Таргетинг на геолокации|
|mobile_apps|string|`readable` `writable` `choices =`
  - `never_installed` - Не устанавливалось никогда 
  - `now` - Установлено сейчас 
  - `deleted` - Удалено сейчас|Установленность приложений|
|mobile_operation_systems|list of integer|`readable` `writable` `max_value=2147483647`|Мобильные операционные системы. [Список доступных ОС](../resource/MobileOperationSystem)|
|mobile_operators|list of integer|`readable` `writable` `min_value=-2147483647` `max_value=2147483647`|Операторы мобильной связи. [Список доступных операторов](../resource/MobileOperator)|
|mobile_prefix|list of string|`readable` `writable`|Мобильные префиксы. Доступные префиксы: mts, beeline, megafon|
|mobile_types|list of string|`readable` `writable`|Типы мобильных устройств. [Список доступных устройств](../resource/MobileTypes)|
|mobile_vendors|list of integer|`readable` `writable` `max_value=2147483647`|Производители мобильных устройств. [Список доступных производителей](../resource/MobileVendors)|
|pad_category|[PadCategoryTargeting](../object/PadCategoryTargeting)|`readable` `writable`|Таргетинг на категорию приложения|
|pads|list of id|`readable` `writable` `min_value=1` `max_value=2147483647`|Рекламные площадки. Доступные площадки определены в пакете кампании|
|regions|list of integer|`readable` `writable` `min_value=-2147483647` `max_value=2147483647`|Регионы (список идентификаторов регионов). [Список доступных регионов](../resource/Region)|
|segments|list of integer|`readable` `writable` `min_value=-2147483647` `max_value=2147483647`|Вхождение в [аудиторные сегменты](../resource/Segments)|
|sex|list of string|`readable` `writable`|Пол (сочетания ‘male’ — мужской, ‘female’ — женский)|
|mobile_operation_systems_sk_ad_network|[MobileOperatingSystemsSkAdNetworkTargeting](../object/MobileOperatingSystemsSkAdNetworkTargeting)|`readable` `writable`|Таргетинг на iOS 14.5+ через `SkAd Network`|
|device_types|list of string|`readable` `writable`|Таргетинг по девайсам ('desktop' — 1, 'mobile' — 2)|