# OrdSubAgent

> Оригинал: [https://ads.vk.com/doc/api/object/OrdSubAgent](https://ads.vk.com/doc/api/object/OrdSubAgent)

---

Объект, предоставляющий информацию о подрядчике клиента агентства.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|contract_date|date|`readable` `writable` `default_field` `min_value=1900-01-01` `max_value=2037-09-04`|Дата договора|
|contract_number|string|`readable` `writable` `default_field` `max_length=255`|Номер договора|
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
|inn|string|`readable` `writable` `default_field``min_length=10` `max_length=12`Заполняется только для российских физ. и юр.лиц|Номер ИНН|
|name|string|`readable` `writable` `default_field``max_length=255`|Название или ФИО|
|user_type|string|`readable` `writable` `default_field` `choices =`
  - `physical` - Физ.лицо резидент 
  - `juridical` - Юр.лицо резидент 
  - `ip` - Юр.лиц ИП резидент 
  - `foreign_physical` - Физ.лицо нерезидент 
  - `foreign_juridical` - Юр.лицо нерезидент|Тип подрядчика|
|vat|boolean|`readable` `writable` `default_field`|Признак плательщика НДС|
|foreign_oksm_country_code|string|`readable` `writable` `max_length=3``min_length=3`Заполняется для user_type foreign_juridical и foreign_physical|Код страны по справочнику [ОКМС](https://classifikators.ru/oksm)|
|foreign_epayment_method|string|`readable` `writable` `max_length=32``min_length=1`Заполняется для user_type foreign_physical|Номер карты или расчётного счёта иностранного электронного средства платежа|
|foreign_inn|string|`readable` `writable` `max_length=50``min_length=1`Заполняется для user_type foreign_juridical|Аналог номера налогоплательщика в стране нерезидента|
|foreign_registration_number|string|`readable` `writable` `max_length=32``min_length=1`Заполняется для user_type foreign_juridical, поле должно быть заполнено, если не заполнено поле foreign_inn|Регистрационный номер компании в стране нерезидента|
|chain_break|boolean|`readable` `writable``default_field`Может иметь только предпоследний участник цепочки|Признак разрыва цепочки|