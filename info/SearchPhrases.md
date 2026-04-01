# SearchPhrases

> Оригинал: [https://ads.vk.com/doc/api/info/SearchPhrases](https://ads.vk.com/doc/api/info/SearchPhrases)

---

### Контекстный таргетинг

действие
метод
запрос
параметры

Создать поисковые фразы
POST
/api/v3/search_phrases.json?name=&lt;name&gt;
name&nbsp;- имя нового списка,&nbsp;

Посмотреть поисковые фразы
GET
/api/v3/search_phrases/&lt;id&gt;.json
id&nbsp;- идентификатор списка

Посмотреть ошибки
GET
/api/v3/search_phrases/&lt;id&gt;.json?errors=1
id&nbsp;- идентификатор списка

Посмотреть все/выбранные списки поисковых фраз
GET
/api/v3/search_phrases.json/api/v3/search_phrases.json?ids=&lt;id1&gt;,...,&lt;idN&gt;
ids - идентификаторы выбранных списков через запятую

Переименовать поисковые фразы
POST
/api/v3/search_phrases/&lt;id&gt;/rename.json?name=&lt;name&gt;
id&nbsp;- идентификатор списка&nbsp;name&nbsp;- новое имя списка

Изменить поисковые фразы
PUT
/api/v3/search_phrases/&lt;id&gt;.json?
id&nbsp;- идентификатор списка,&nbsp;

Удалить поисковые фразы
DELETE
/api/v3/search_phrases/&lt;id&gt;.json
id&nbsp;- идентификатор списка

Скачать исходный csv-файл
GET
/api/v3/search_phrases/&lt;id&gt;.csv
id&nbsp;- идентификатор списка

Создание списка контекстных фраз

Запрос POST&nbsp;

/api/v3/search_phrases.json?name=&lt;name&gt;

Параметры:

name - имя нового списка

Пример запроса:

Request URL: https://ads.vk.com/api/v3/search_phrases.json?name=my_test_list
Request Method: POST
Request Heders:
 Content-Type: text/csv; charset=UTF-8;
 X-Trg-User-Id: &lt;здесь айди пользователя&gt;

Тело запроса:
phrase,expires
one,12d
two,12d
three,12d

Пример запроса json:

Request URL: https://ads.vk.com/api/v3/search_phrases.json?name=my_test_list
Request Method: POST
Request Heders:
 Content-Type: Content-Type: application/json;
 X-Trg-User-Id: &lt;здесь айди пользователя&gt;

Тело запроса:

{

&nbsp;&nbsp;&nbsp;&nbsp;"phrases":["one,two,three"],

&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases":&nbsp;:[sheep],

&nbsp;&nbsp;&nbsp;&nbsp;"expires":&nbsp;:"12d",

&nbsp;&nbsp;&nbsp;&nbsp;"category": "test"

}

Пример успешного ответа

{

&nbsp;&nbsp;&nbsp;&nbsp;"id": 1,&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// id созданного списка

&nbsp;&nbsp;&nbsp;&nbsp;"name":&nbsp;"test",

&nbsp;&nbsp;&nbsp;&nbsp;"status":&nbsp;"ready",

&nbsp;&nbsp;&nbsp;&nbsp;"phrases_cnt": 4,

&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases_cnt": 6,

&nbsp;&nbsp;&nbsp;&nbsp;"errors_cnt": 3,&nbsp;// количество ошибок (нераспарсенных строк)

&nbsp;&nbsp;&nbsp;&nbsp;"created":&nbsp;"2018-01-24T11:17:59+03:00",

&nbsp;&nbsp;&nbsp;&nbsp;"updated":&nbsp;"2018-01-24T14:35:50+03:00"

&nbsp;&nbsp;&nbsp;&nbsp;"category":&nbsp;"test"

}

Задать и получить в ответе поле "category" возможно только при наличии дополнительного права.

Пример ответа с превышением лимита количества фраз

{
&nbsp;&nbsp;&nbsp;&nbsp;"error": {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message":&nbsp;"limit 1 exceeded",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"code": 1008,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"details": {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limit": 1
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;}
}

Посмотреть список контекстных фраз

Запрос GET

/api/v3/search_phrases/&lt;id&gt;.json

Параметры:

id&nbsp;- идентификатор списка

Пример ответа

{
&nbsp;&nbsp;&nbsp;&nbsp;"errors_cnt": 3,
&nbsp;&nbsp;&nbsp;&nbsp;"items": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"phrase":&nbsp;"Купить пластиковые окна",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases": [&nbsp;"межкомнатные двери",&nbsp;"в европу",&nbsp;"сейчас или никогда"],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"price_coeff": 1,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"expires": 7200,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"fading":&nbsp;"inverse",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sub":&nbsp;"Купить пластиковые окна"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"phrase":&nbsp;"Продать гараж срочно",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases": [&nbsp;"дом",&nbsp;"снять квартитру"&nbsp;],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"price_coeff": 0.8,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"expires": 86520,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"fading":&nbsp;"linear",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sub":&nbsp;"гараж"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"phrase":&nbsp;"подарки",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases": [ ],
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"price_coeff": 1,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"expires": 864000,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"fading":&nbsp;"const",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sub":&nbsp;"подарки"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;]
}

Посмотреть ошибки

Запрос GET

/api/v3/search_phrases/&lt;id&gt;.json?errors=1

Пример ответа

{
&nbsp;&nbsp;&nbsp;&nbsp;"items": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"line_number": 5,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"source_line":&nbsp;",",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message":&nbsp;"'phrase' is empty",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"code": 1002
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"line_number": 6,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"source_line":&nbsp;"$OS, 1d",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message":&nbsp;"'phrase' bad format",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"code": 1003
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"line_number": 8,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"source_line":&nbsp;"билеты, 1d2h3",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message":&nbsp;"'expires' bad format",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"code": 1006
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
&nbsp;&nbsp;&nbsp;&nbsp;]
}

Посмотреть все/выбранные списки контекстных фраз

Запрос GET

/api/v3/search_phrases.json

/api/v3/search_phrases.json?ids=&lt;id1&gt;,...,&lt;idN&gt; 

Параметры:

ids - идентификаторы выбранных списков через запятую

Пример ответа
{
&nbsp;&nbsp;&nbsp;&nbsp;"items": [
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": 1,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name":&nbsp;"продажа",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"status":&nbsp;"ready",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"phrases_cnt": 42,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases_cnt": 5,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"errors_cnt": 4,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"created":&nbsp;"2017-12-22T11:02:27+03:00",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"updated":&nbsp;"2017-12-22T14:02:27+03:00",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"category": "test"

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": 2,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name":&nbsp;"покупка",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"status":&nbsp;"ready",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"phrases_cnt": 9,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases_cnt": 0,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"errors_cnt": 0,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"created":&nbsp;"2017-12-23T10:03:45+03:00",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"updated":&nbsp;
"2017-12-23T10:03:45+03:00"
,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"category": "test"

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
&nbsp;&nbsp;&nbsp;&nbsp;]
}

Переименовать поисковые фразы

Запрос POST

/api/v3/search_phrases/&lt;id&gt;/rename.json?name=&lt;name&gt;

Параметры:

id&nbsp;- идентификатор спискаname&nbsp;- новое имя списка

Изменить поисковые фразы

PUT запрос:

/api/v3/search_phrases/&lt;id&gt;.json

Параметры:

id&nbsp;- идентификатор списка

Так же доступно изменение с помощью json.

Тело запроса:

{

&nbsp;&nbsp;&nbsp;&nbsp;"phrases":["one,two,three"],

&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases":&nbsp;:[sheep],

&nbsp;&nbsp;&nbsp;&nbsp;"expires":&nbsp;:"12d",

&nbsp;&nbsp;&nbsp;&nbsp;"category": "test"

}

Пример ответа
{
&nbsp;&nbsp;&nbsp;&nbsp;"id": 1,
&nbsp;&nbsp;&nbsp;&nbsp;"name":&nbsp;"продажа",
&nbsp;&nbsp;&nbsp;&nbsp;"status":&nbsp;"ready",
&nbsp;&nbsp;&nbsp;&nbsp;"phrases_cnt": 42,
&nbsp;&nbsp;&nbsp;&nbsp;"stop_phrases_cnt": 5,
&nbsp;&nbsp;&nbsp;&nbsp;"errors_cnt": 0,
&nbsp;&nbsp;&nbsp;&nbsp;"created":&nbsp;"2017-12-22T11:02:27+03:00",
&nbsp;&nbsp;&nbsp;&nbsp;"updated"
:&nbsp;"2017-12-26T19:03:22+03:00",
}

Удалить поисковые фразы

Запрос DELETE:

/api/v3/search_phrases/&lt;id&gt;.json

Параметры:

id&nbsp;- идентификатор списка

Cкачать исходный CSV-файл

Запрос GET

/api/v3/search_phrases/&lt;id&gt;.csv

Параметры:

id&nbsp;- идентификатор списка

Возвращаемые ошибки

Все ошибочные ответы возвращаются так:

{

&nbsp;&nbsp;&nbsp;&nbsp;"error": {

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"code":&nbsp;"ERROR_CODE",

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message":&nbsp;"message text"

&nbsp;&nbsp;&nbsp;&nbsp;}

}

http status

code&nbsp;

message&nbsp;

400 Bad Request

ERROR&nbsp;

can't read request body&nbsp;

400 Bad Request&nbsp;

BAD_DATA&nbsp;

bad csv header&nbsp;
column 'phrase' is mandatory&nbsp;
bad csv file&nbsp;

404 Not Found&nbsp;

NOT_FOUND&nbsp;

search phrases not found&nbsp;

409 Conflict&nbsp;

WAIT_TIMEOUT

search phrases locked&nbsp;

410 Gone

DELETED&nbsp;

search phrases not found&nbsp;

410 Gone

NOT_READY&nbsp;

search phrases not ready&nbsp;

413 Request Entity Too Large&nbsp;

ERROR&nbsp;

too many phrases in the list&nbsp;

500 Internal Server Error&nbsp;

ERROR&nbsp;