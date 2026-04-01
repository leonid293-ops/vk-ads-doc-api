# URL

> Оригинал: [https://ads.vk.com/doc/api/object/URL](https://ads.vk.com/doc/api/object/URL)

---

Объект рекламируемой ссылки.

Используется в методах: [CreateUrl](../resource/CreateUrl), [ReadUrls](../resource/ReadUrls), [ReadUrl](../resource/ReadUrl)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|counters|list of string|`readable` `default_field`|Счетчики, найденные на лендинге ссылки. Примеры значений: TOP_MAIL_RU, RAMBLER_TOP100, GOOGLE_ANALYTICS, YA_METRICA, LI_RU|
|has_goals|boolean|`readable` `default_field`|Флаг, определяющий достаточно ли конверсий лидов в установки собрало рекламируемое по ссылке приложение, чтобы можно было создать рекламную кампанию с оплатой за установки|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|ID созданного объекта|
|preview_link|string|`readable`|Ссылка предварительного просмотра, если он доступен|
|url|url|`readable` `required` `writable` `default_field`|Ссылка, обязательно в схеме http:// или https://|
|url_types|list of string|`readable` `default_field`|Типы ссылки, которые были определены автоматически. Для использования в рекламных объявлениях ссылка должна содержать тип, указанный в [баннерном формате](../object/BannerFormat) в поле "fields"|