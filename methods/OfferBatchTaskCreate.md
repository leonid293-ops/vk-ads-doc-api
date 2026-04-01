# OfferBatchTaskCreate

> Оригинал: [https://ads.vk.com/doc/api/resource/OfferBatchTaskCreate](https://ads.vk.com/doc/api/resource/OfferBatchTaskCreate)

---

## /api/v2/remarketing/pricelists/
/batch.json

Метод для пакетного создания, обновления и удаления продуктов в каталоге без полной загрузки фида. 

Для проверки результата выполнения используется [OfferBatchTaskDetail](../resource/OfferBatchTaskDetail)

### Получение доступа к API

Для начала работы с API нужно переключить тип источника каталога на  «‎Обновление по API»‎. Сделать это можно, обратившись в техподдержку.

Каталог будет исключен из расписания периодических обкачек из источника, все обновления будут происходить посредством API.

### POST

Постановка задачи на пакетное обновление товаров. Тело запроса представляет собой текст, состоящий из JSON-объектов, разделенных переносом строки (Newline Delimited JSON). Переносы строки внутри JSON-объектов недопустимы.

Ограничение на размер тела запроса: 200 МБ.

Задачи на обновление будут выполняться последовательно в порядке создания.

Каждый JSON-объект содержит 2 поля: method - тип действия и data - поля изменяемого продукта.

``` HTTP 
{"method": "", "data":}
{"method": "", "data":}
{"method": "", "data":}
```

Поддерживаемые значения атрибута `method`:

* `PUT` &ndash; создание или обновление всех атрибутов продукта. Объект `data` содержит полный набор новых атрибутов создаваемого или обновляемого продукта (он будет полностью заменен в базе).
* `DELETE` &ndash; удаление продукта. В объекте `data` необходимо наличия только атрибута `id` с идентификатором удаляемого продукта.

Возможные коды ответа:

- 201 &ndash; задача поставлена в очередь.
- 400 &ndash; ошибка валидации формата запроса или слишком большой запрос.
- 404 &ndash; каталог не найден или не имеет типа источника «‎Обновление по API».

Названия атрибутов полностью соответствуют поддерживаемым в фиде формата CSV атрибутам. Поддерживаемые атрибуты (пример) &ndash; разделители строки для удобства чтения, в запросе из быть не должно:

``` HTTP
{
   "id":"DB_1",
   "title":"Dog Bowl In Blue",
   "ios_url":"example://electronic/db_1",
   "ios_app_store_id":"123",
   "ios_app_name":"Electronic Example iOS",
   "android_url":"example://electronic/db_1",
   "android_package":"com.electronic.example",
   "android_app_name":"Electronic Example Android",
   "windows_phone_url":"example-windows://electronic/db_1",
   "windows_phone_app_id":"64ec0d1b-5b3b-4c77-a86b-5e12d465edc0",
   "windows_phone_app_name":"Electronic Example Windows",
   "description":"Solid plastic Dog Bowl in marine blue color",
   "google_product_category":"Animals > Pet Supplies",
   "product_type":"Bowls & Dining > Food & Water Bowls",
   "link":"http://www.example.com/bowls/db-1.html",
   "image_link":"https://www.example.com/images/product_image_template.png?id=1",
   "condition":"new",
   "availability":"in stock",
   "price":"300.99 RUR",
   "sale_price":"",
   "sale_price_effective_date":"",
   "gtin":"",
   "brand":"Example",
   "mpn":"",
   "item_group_id":"DB_GROUP_1",
   "gender":"",
   "age_group":"",
   "color":"",
   "size":"",
   "shipping":"UK::Standard:9.95 EUR",
   "custom_label_0":"Made in Waterford, IE",
   "additional_image_link":"https://test.com/add_img1,https://test.com/add_img2"
}
```

Пример запроса:

``` HTTP
POST /api/v2/remarketing/pricelists/
/batch.json
{"method": "PUT", "data":{"id": "offer1", "product_type": "category1", "title": "Offer1","link": "http://example.org/1", "image_link": "http://example.org/1.jpg", "price": "100 RUB"}}
{"method": "PUT", "data":{"id": "offer2", "product_type": "category2", "title": "Offer2","link": "http://example.org/2", "image_link": "http://example.org/2.jpg", "price": "200 RUB"}}
{"method": "DELETE", "data":{"id": "offer3"}}
```

В данном примере обновляются данные для продуктов offer1 и offer2, удаляется offer3.

Пример ответа:

``` HTTP
HTTP 201
[
    {"id": 6, "status": "pending"}
]
````

### GET

Список выполняющихся и недавно завершенных задач и их статусы.

``` HTTP
GET /api/v2/remarketing/pricelists/
/batch.json
```

Пример ответа:

``` HTTP
{
    "items": [
        {
            "id": 1,
            "status": "done"
        },
        {
            "id": 3,
            "status": "error"
        },
        {
            "id": 5,
            "status": "process"
        },
        {
            "id": 6,
            "status": "pending"
        },
        {
            "id": 7,
            "status": "pending"
        }
    ]
}
```

В примере выше: задача 1 выполнилась (в том числе, с ошибками и предупреждениями), 3 &ndash; провалилась, 5 &ndash; выполняется в текущий момент, 6 и 7 &ndash; ожидают своей очереди.

Возможные коды ответа:

- 200 &ndash; список задач, относящихся к каталогу.
- 404 &ndash; каталог не найден или не имеет типа источника «‎Обновление по API».

Детализацию по результату выполнения можно запросить в [OfferBatchTaskDetail](../resource/OfferBatchTaskDetail).