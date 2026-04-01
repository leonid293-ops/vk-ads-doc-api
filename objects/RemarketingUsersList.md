# RemarketingUsersList

> Оригинал: [https://ads.vk.com/doc/api/object/RemarketingUsersList](https://ads.vk.com/doc/api/object/RemarketingUsersList)

---

Источник данных - список пользователей.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|base|integer|`readable` `writable` `default_field` `create_only` `min_value=-2147483647` `max_value=2147483647`|Идентификатор базового списка, используется для обновления данных в списках.  Возможные варианты: - "base" = 0 - этот базовый список; - "base = N" - к списку N добавятся ID загружаемого списка; - "base = -N" - из списка N будут удалены ID загружаемого списка|
|created|datetime|`readable` `default_field`|Время создания списка|
|entries_count|integer|`readable` `default_field` `min_value=-2147483647` `max_value=2147483647`|Количество загруженных элементов из списка|
|has_history|boolean|`readable` `default_field`|Наличие истории изменений базового списка|
|history|list of [RemarketingUsersListHistory](../object/RemarketingUsersListHistory)|`readable`|История изменений базового списка|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор списка|
|ids_count|integer|`readable` `default_field` `min_value=-2147483647` `max_value=2147483647`|Исходный размер списка|
|matched_ids_count|integer|`readable` `default_field` `min_value=-2147483647` `max_value=2147483647`|Количество исходных ID, для которых были найдены соответствия|
|name|string|`readable` `required` `writable` `default_field`|Название списка|
|status|string|`readable` `default_field` `choices =`
  - `receiving` - Список в процессе принятия на загрузку (статус по умолчанию) 
  - `received` - Список принят для загрузки 
  - `mapping` - Список обрабатывается (происходит сопоставление) 
  - `mapped` - Список обработан 
  - `writing` - Обработанный список в процессе записи в базу данных 
  - `ready` - Список записан и готов к использованию 
  - `pending_delete` - Список отмечен пользователем к удалению 
  - `deleting` - Список удаляется из базы данных 
  - `deleted` - Список удален 
  - `deleted_to_notify` - Список удален по инициативе VK Ads, но пользователь еще не подтвердил, что знает об этом|Статус обработки|
|type|string|`readable` `required` `writable` `default_field` `create_only` `choices =`
  - `ok` - Список ID пользователей соцсети Одноклассники 
  - `mm` - Список игровых ID пользователей соцсети Мой Мир 
  - `phones` - Список телефонных номеров или их хешей 
  - `emails` - Список электронных почтовых адресов или их хешей 
  - `device_id` - Список аппаратных идентификаторов устройств Android 
  - `android_id` - Список программных идентификаторов устройств Android 
  - `advertising_id` - Список Google Advertising ID 
  - `idfa` - Список идентификаторов мобильных устройств Apple 
  - `dmp_id` - Список внешних ID пользователей из партнёрских DMP-провайдеров 
  - `dmp_top` - Список first-party data идентификаторов 
  - `vk` - Список ID пользователей соцсети ВКонтакте 
  - `mac` - Список MAC-адресов 
  - `mparticle` - Список пользователей mParticle 
  - `human` - Единый список позволяет загружать несколько видов идентификаторов в одном файле|Тип списка. Подробнее о разных типах списков можно прочитать [здесь](https://target.my.com/adv/help/remarketing/#user_list)|
|updated|datetime|`readable`|Время изменения списка|
|users|list of [RemarketingUsersListUser](../object/RemarketingUsersListUser)|`readable`|Пользователи, обладающие доступом к списку|
|users_count|integer|`readable` `min_value=-2147483647` `max_value=2147483647`|Количество пользователей, обладающих доступом к списку|