# Content

> Оригинал: [https://ads.vk.com/doc/api/resource/Content](https://ads.vk.com/doc/api/resource/Content)

---

## /api/v2/content/(static|video|html5).json

Ресурс, позволяющий загружать креативы, которые в дальнейшем могут быть использованы в рекламных объявлениях. Креативы, загруженные с помощью данного ресурса, могут быть использованы только в тех пакетах, в баннерном формате которых есть секция "content".

Используется объект: [Content](../object/Content)

### POST

Запрос должен иметь тип multipart/form-data. Для методов static.json и video.json в структуре "data" требуется обязательно указать ширину и высоту исходного креатива в параметрах ("width" и "height" соответственно).

Статичные изображения должны загружаться по адресу https://ads.vk.com/api/v2/content/static.json.

Видео должны загружаться по адресу https://ads.vk.com/api/v2/content/video.json.

HTML5-креативы должны загружаться по адресу https://ads.vk.com/api/v2/content/html5.json.
Для этого метода достаточно указать файл, соответствующий требованиям к HTML-5 баннерам (https://sales.mail.ru/ru/russia/main/latest/technical/#a75).

Пример запроса:

```HTTP

   curl -X POST -H "Authorization: Bearer LIDM…Io4Qj"  -H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" -F "file=@[object Object]" -F 'data={"width":1612, "height":980}' "https://ads.vk.com/api/v2/content/static.json"
```

Пример ответа:

```HTTP

    {
       "variants": {
           "original": {
               "url": "https://r.mradx.net/img/17/B36CF7.jpg",
               "width": 90,
               "height": 75,
               "size": 3339
           }
       },
       "id": 1084236
   }
```

Все ошибки имеют вид:

```HTTP

    {
        "error": {
            "code": "validation_failed",
            "fields": {
                "file": ""
            },
            "message": "Validation failed"
        }
    }
```

Возможные ошибки для static.json и video.json:

- {"code": "format_not_supported", "message": "Unsupported content format."}
- {"code": "cannot_upload", "message": "Cannot upload content"}
- {"code": "no_file", "message": "Content not found in the request. Request must have multipart/form-data type with "file" field."}
- {"code": "broken_content", "message": "Content is broken"}
- {"code": "content_too_large", "message": "Content is too large"}
- {"code": "content_bad_size", "message": "Content has bad size"}

Возможные коды ошибок для html5.json:

- bad_archive - ошибка при открытии zip архива;
- no_html_file - архив не содержит html файл; 
- too_many_html_files - архив содержит больше одного html файла; 
- invalid_file_name - некорректное имя html файла; 
- tag_unclosed - незакрытый тэг; 
- wrong_symbols - в ссылке содержатся некорректные символы; 
- incorrect_ad_size - размер креатива не установлен в ; 
- href_not_found - тэг "a" должен иметь аттрибут "href"; 
- null_symbol - html файл содержит NULL символ; 
- external_css - внешний CSS содержит ссылки на ресурсы; 
- validation_error - ошибка валидации API v2; 

Подробности ошибок описаны в поле "message".