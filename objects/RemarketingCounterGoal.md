# RemarketingCounterGoal

> Оригинал: [https://ads.vk.com/doc/api/object/RemarketingCounterGoal](https://ads.vk.com/doc/api/object/RemarketingCounterGoal)

---

Цель счетчика.

Используется в методах: [CounterGoals](../resource/CounterGoals), [CounterGoal](../resource/CounterGoal)

Используется в объектах: [RemarketingCounter](../object/RemarketingCounter)

|Field name|Type|Conditions|Description|
|-|-|-|-|
|condition|string|`readable` `required` `writable` `create_only` `choices =`
  - `uss` - Подстрока в URL. 
  - `rss` - Подстрока в Referer. 
  - `jse` - Событие из JS. 
  - `hd` - Глубина просмотра (минимум 2). 
  - `ts` - Время на сайте.|Тип условия для достижения цели.|
|goal_type|string|`readable` `writable` `choices =`
  - `content` - Просмотр материалов. 
  - `search` - Поиск. 
  - `basket` - Добавление в корзину. 
  - `wishlist` - Добавление в список желаний. 
  - `checkout` - Инициация оформления заказа. 
  - `payment_info` - Добавление платежной информации. 
  - `purchase` - Покупка. 
  - `lead` - Лид. 
  - `registration` - Выполнение регистрации. 
  - `custom` - Пользовательские конверсии.|Тип цели (обязателен для целей, не являющихся пикселями).|
|id|id|`readable` `default_field` `min_value=1` `max_value=2147483647`|Идентификатор цели.|
|name|string|`readable` `required` `writable`|Название цели.|
|substr|string|`readable` `required` `writable` `create_only`|Строка условия цели (substr или substr_uss, substr_rss, …).|
|value|integer|`readable` `writable` `min_value=-2147483647` `max_value=2147483647`|Значение цели (сколько было достижений).|