# OfferBatchTaskDetail

> Оригинал: [https://ads.vk.com/doc/api/resource/OfferBatchTaskDetail](https://ads.vk.com/doc/api/resource/OfferBatchTaskDetail)

---

## /api/v2/remarketing/pricelists/
/batch/.json

Метод для получения детальной информации по задаче пакетного создания, обновления и удаления продуктов в каталоге. 

Для постановки задач используется [OfferBatchTaskCreate](../resource/OfferBatchTaskCreate)

Отчёт об ошибках при валидации доступен по адресу

```
GET /api/v2/remarketing/pricelists/
/batch/.json
```

Пример ответа:

``` HTTP
{
   "errors":[
      {
         "code":"JSON_LINE_DECODE_ERROR",
         "count":1,
         "errors":[
            {
               "comment":"",
               "created":"2022-08-30 17:01:24",
               "element":null,
               "message":"Ошибка в формате строки JSON",
               "offer_id":"",
               "offer_name":"",
               "pricelist_id":26825
            }
         ],
         "event":"feed_failure",
         "field":"",
         "last_start_ts":1661868084,
         "pricelist_id":26825
      },
      {
         "code":"DYNAMIC_IMAGES_PICTURE_NOT_FOUND",
         "count":1,
         "errors":[
            {
               "comment":"",
               "created":"2022-08-30 17:01:24",
               "element":"http://example.org/1.jpg",
               "message":"При загрузке изображения получена ошибка HTTP 404 Not found",
               "offer_id":"o1",
               "offer_name":"",
               "pricelist_id":26825
            }
         ],
         "event":"offer_error",
         "field":"picture",
         "last_start_ts":1661868084,
         "pricelist_id":26825
      }
   ],
   "id":10,
   "status":"done"
}
```

В ответе `errors` содержит список ошибок и предупреждений, обнаруженных при обработке файла. Для каждой из ошибок указывается:

* `event` &ndash; уровень ошибки;
*  `code` &ndash; код ошибки;
* `field` &ndash;  название атрибута, в котором произошла ошибка;
* `count` &ndash; количество ошибок такого типа;
* `errors` &ndash; частные примеры ошибок 

Атрибут `event` может принимать значения:

* `feed_failure` &ndash; критическая ошибка, не позволяющая обработать задачу целиком. Например, неправильный формат данных, битый JSON и т.д.
* `offer_error` &ndash; ошибка, из-за которой товар не был сохранен с указанием проблемы
* `offer_warning` &ndash; товар сохранен, но с некоторыми неточностями или допущениями, либо есть рекомендации по улучшению описания и метаданных.

Возможные коды ответа:

- 200 &ndash; задача найдена
- 404 &ndash; каталог или задача не найдены, либо каталог не имеет типа источника «‎Обновление по API».