# OrdUser

> Оригинал: [https://ads.vk.com/doc/api/object/OrdUser](https://ads.vk.com/doc/api/object/OrdUser)

---

Объект, хранящий ОРД данные пользователя физ. лица.

Используется в объектах: [User](../object/User)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|name|string|`readable` `writable`|Наименование|
|phone|string|`readable` `writable`|Номер телефона|
|inn|string|`readable` `writable`|Инн|
|foreign_epayment_method|string|`readable` `writable`|Номер карты или расчётного счёта иностранного электронного средства платежа|
|foreign_oksm_country_code|string|`readable` `writable` `default_field`|Код страны в цифровом формате ISO 316|
|foreign_registration_number|string|`readable` `writable`|Регистрационный номер иностранного юридического лица|
|foreign_inn|string|`readable` `writable`|Номер налогоплательщика или его аналог, присвоенный в стране регистрации|
|site|string|`readable` `writable`|Адрес сайта|e5:T18122,