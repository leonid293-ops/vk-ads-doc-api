# SegmentParams

> Оригинал: [https://ads.vk.com/doc/api/info/SegmentParams](https://ads.vk.com/doc/api/info/SegmentParams)

---

### Параметры источников данных в сегментах

  - Список пользовательских идентификаторов

table {
  width: 0 !important
}

Общие параметры:

  
    type
    	Условие показа объявления
    positive — для входящих в источник
negative — для не входящих в источник
  

Общие параметры для временных интервалов:

  
    right
    Начало временного интервала, указывается в виде количества дней до запроса
    0 &lt;= right &lt;= 365, left &gt;right
  
  
    left
    Окончание временного интервала, указывается в виде количества дней до запроса
    0 &lt;= left &lt;= 365, left &gt;right
  

Список пользовательских идентификаторов
Позволяет включить в сегмент аудитории пользователей из загруженного в VK Ads списка.

object_type: remarketing_users_list

Источник: [RemarketingUsersList](../object/RemarketingUsersList)

Временной интервал: Нет

Параметры:

  
    source_id	
    ID списка пользователей (RemarketingUsersList.id)
  

Пример:

```HTML
{
    "object_type":"remarketing_users_list",
    "params":{
        "source_id":28612,
        "type":"positive"
    }
}
```ce:T254f,