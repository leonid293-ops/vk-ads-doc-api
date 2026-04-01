# ClientOrdPhysical

> Оригинал: [https://ads.vk.com/doc/api/object/ClientOrdPhysical](https://ads.vk.com/doc/api/object/ClientOrdPhysical)

---

Объект, предоставляющий информацию о данных клиента агентства (физического лица) для ОРД.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|contract_date|date|`readable` `writable` `min_value=1900-01-01` `max_value=2037-09-04`|Дата договора|
|contract_number|string|`readable` `writable` `max_length=255`|Номер договора|
|contract_subject|string|`readable` `writable` `default_field` `choices =`
  - `representation` - Представительство 
  - `distribution` - Договор на распространение рекламы 
  - `org_distribution` - Договор на организацию распространения рекламы 
  - `mediation` - Посредничество 
  - `other` - Иное|Сведения о предмете договора|
|contract_type|string|`readable` `writable` `default_field` `choices =`
  - `service` - Договор оказания услуг 
  - `mediation` - Посреднический договор 
  - `additional` - Дополнительное соглашение|Тип контракта|
|inn|string|`readable` `writable` `min_length=10` `max_length=12`|Номер ИНН|
|name|string|`readable` `writable``max_length=255`|ФИО|
|phone|string|`readable` `writable``min_length=8` `max_length=15`|Номер телефона|
|sub_agents|list of [OrdSubAgent](../object/OrdSubAgent)|`readable` `writable` `default_field`|Подрядчики|
|user_type|string|`readable` `writable` `choices =`
  - `physical` - Физ.лицо резидент|Тип клиента|
|vat|boolean|`readable` `writable`|Признак плательщика НДС|

Объект, предоставляющий информацию о данных клиента агентства (иностранного физического лица) для ОРД.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|contract_date|date|`readable` `writable` `min_value=1900-01-01` `max_value=2037-09-04`|Дата договора|
|contract_number|string|`readable` `writable` `max_length=255`|Номер договора|
|contract_subject|string|`readable` `writable` `default_field` `choices =`
  - `representation` - Представительство 
  - `distribution` - Договор на распространение рекламы 
  - `org_distribution` - Договор на организацию распространения рекламы 
  - `mediation` - Посредничество 
  - `other` - Иное|Сведения о предмете договора|
|contract_type|string|`readable` `writable` `default_field` `choices =`
  - `service` - Договор оказания услуг 
  - `mediation` - Посреднический договор 
  - `additional` - Дополнительное соглашение|Тип контракта|
|foreign_oksm_country_code|string|`readable` `writable` `min_length=3` `max_length=3`|Код страны по справочнику [ОКМС](https://classifikators.ru/oksm)|
|foreign_epayment_method|string|`readable` `writable` `min_length=1` `max_length=32`Должно быть заполнено, если не заполнено поле phone|Номер карты или расчётного счёта иностранного электронного средства платежа|
|name|string|`readable` `writable``max_length=255`|ФИО|
|phone|string|`readable` `writable``min_length=8` `max_length=15`|Номер телефона|
|sub_agents|list of [OrdSubAgent](../object/OrdSubAgent)|`readable` `writable` `default_field`|Подрядчики|
|user_type|string|`readable` `writable` `choices =`
  - `foreign_physical` - Физ.лицо нерезидент|Тип клиента|
|vat|boolean|`readable` `writable`|Признак плательщика НДС|