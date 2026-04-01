# ProjectionPrediction

> Оригинал: [https://ads.vk.com/doc/api/object/ProjectionPrediction](https://ads.vk.com/doc/api/object/ProjectionPrediction)

---

Объект, содержащий информацию о прогнозе охвата аудитории в зависимости от стоимости события.

Используется в методах: [ProjectionPrediction](../resource/ProjectionPrediction)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|campaign_id|id|`writable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор рекламной группы. Только для запроса.|
|cr_ctr|list of [PredictedRate](../object/PredictedRate)|`readable`|Список cr/ctr для пакета и идентификатора гистограммы, соответсвующей данному пакету. Только в ответе.|
|histograms|list of [Histogram](../object/Histogram)|`readable`|Список гистограмм с ценами/охватами. Только в ответе. Одна и та же гистограмма может соответствовать разным пакетам, соответствующая определяется по идентификатору гистограммы в поле cr_ctr. Только в ответе.|
|package_ids|list of integer|`writable` `min_value=-2147483647` `max_value=2147483647`|Список ID пакетов. Только для запроса.|
|targetings|[ProjectionTargetings](../object/ProjectionTargetings)|`required` `writable`|Таргетинги для расчета охвата. Только для запроса.|dd:T5f8,Информация о прогнозируемом CR и CTR для пакета или рекламной групп