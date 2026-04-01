# AgencyClient

> Оригинал: [https://ads.vk.com/doc/api/object/AgencyClient](https://ads.vk.com/doc/api/object/AgencyClient)

---

Объект, предоставляющий информацию о клиенте агентства.

Используется в методах: [AgencyClients](../resource/AgencyClients), [AgencyClient](../resource/AgencyClient)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|is_vkads|boolean|`readable` `writable`|Признак клиента в ВК Рекламе|
|access_type|string|`readable` `required` `writable` `default_field` `choices =`
  - `full_access` - Полный доступ 
  - `readonly` - Только чтение 
  - `fin_readonly` - Без доступа к счету 
  - `ads_readonly` - Только доступ к счету|Тип доступа агентства к учетной записи клиента|
|status|string|`readable` `default_field` `choices =`
  - `active` - Активный 
  - `deleted` - Удаленный 
  - `blocked` - Заблокированный|Статус отношения между клиентом и агенством|
|user|[UserClient](../object/UserClient)|`readable` `writable` `default_field`|Клиент|
|juridical_details|[ClientOrdJuridical](../object/ClientOrdJuridical)|`readable` `writable`|Данные клиента юр.лица для ОРД|
|physical_details|[ClientOrdPhysical](../object/ClientOrdPhysical)|`readable` `writable`|Данные клиента физ.лица для ОРД|