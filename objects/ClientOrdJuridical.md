# ClientOrdJuridical

> Оригинал: [https://ads.vk.com/doc/api/object/ClientOrdJuridical](https://ads.vk.com/doc/api/object/ClientOrdJuridical)

---

Объект, предоставляющий информацию о данных клиента агентства (юридического лица, зарегистрированного на территории РФ) для ОРД.

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
|name|string|`readable` `writable``max_length=255`|Название|
|sub_agents|list of [OrdSubAgent](../object/OrdSubAgent)|`readable` `writable` `default_field`|Подрядчики|
|user_type|string|`readable` `writable` `choices =`
  - `juridical` - Юр.лицо резидент 
  - `ip` - Юр.лиц ИП резидент |Тип клиента|
|vat|boolean|`readable` `writable`|Признак плательщика НДС|

Объект, предоставляющий информацию о данных клиента агентства (иностранного юридического лица) для ОРД.

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
|foreign_inn|string|`readable` `writable` `min_length=1` `max_length=50`|Аналог номера налогоплательщика в стране нерезидента|
|foreign_registration_number|string|`readable` `writable` `min_length=1` `max_length=32`Поле должно быть заполнено, если не заполнено поле foreign_inn|Регистрационный номер компании в стране нерезидента|
|name|string|`readable` `writable``max_length=255`|Название|
|sub_agents|list of [OrdSubAgent](../object/OrdSubAgent)|`readable` `writable` `default_field`|Подрядчики|
|user_type|string|`readable` `writable` `choices =` 
  - `foreign_juridical` - Юр.лицо нерезидент |Тип клиента|
|vat|boolean|`readable` `writable`|Признак плательщика НДС|