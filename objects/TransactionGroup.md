# TransactionGroup

> Оригинал: [https://ads.vk.com/doc/api/object/TransactionGroup](https://ads.vk.com/doc/api/object/TransactionGroup)

---

Информация о группе транзакций

Используется в методах: [TransactionGroups](../resource/TransactionGroups)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|amount|decimal|`readable` `default_field`|Сумма|
|client_id|integer|`readable` `default_field` `min_value=-2147483647` `max_value=2147483647`|User ID клиента|
|date|date|`readable`|Месяц (дата в формате YY-MM-01)|
|description|string|`readable` `default_field`|Описание|
|first_at|datetime|`readable` `default_field`|Дата и время первой транзакции в группе|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор|
|invoices|list of integer|`readable` `default_field` `min_value=-2147483647` `max_value=2147483647`|Список идентификаторов счетов|
|is_commercial|boolean|`readable` `default_field`|Группа коммерческих транзакций|
|last_at|datetime|`readable` `default_field`|Дата и время последней транзакции в группе|
|object_id|integer|`readable` `default_field` `max_value=2147483647`|Идентификатор объекта|
|object_type|string|`readable` `default_field` `choices =`
  - `none` - Нет 
  - `campaign` - Кампания 
  - `pad` - Площадка 
  - `tps` - Tps 
  - `user` - Пользователь|Тип объекта|
|payments_total|decimal|`readable` `default_field`|Сумма оплат|
|receipt|url|`readable` `default_field`|Ссылка на фискальный чек|
|tax_amount|decimal|`readable` `default_field`|Сумма НДС|
|type|string|`readable` `default_field` `choices =`
  - `charge` - Списания 
  - `charge_credit` - Кредитные списания 
  - `deposit` - Начисления 
  - `deposit_credit` - Кредитные начисления|Тип|