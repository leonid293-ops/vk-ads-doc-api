# AgencyManagerClient

> Оригинал: [https://ads.vk.com/doc/api/object/AgencyManagerClient](https://ads.vk.com/doc/api/object/AgencyManagerClient)

---

Объект, предоставляющий информацию о клиенте менеджера.

Используется в методах: [AgencyManagerClient](../resource/AgencyManagerClient)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|access_type|string|`readable` `required` `writable` `default_field` `choices =`
  - `full_access` - Полный доступ. 
  - `readonly` - Только чтение. 
  - `fin_readonly` - Без доступа к счету. 
  - `ads_readonly` - Только доступ к счету.|Тип доступа менеджера к учетной записи клиента.|
|status|string|`readable` `default_field` `choices =`
  - `active` - Активный. 
  - `deleted` - Удаленный. 
  - `blocked` - Заблокированный.|Статус отношения между клиентом и менеджером.|
|user|[UserManagerClient](../object/UserManagerClient)|`readable` `writable` `default_field`|Клиент. Возвращается в GET запросе.|5a:T945,