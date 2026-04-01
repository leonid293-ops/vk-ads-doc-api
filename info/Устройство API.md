# Устройство API

> Оригинал: [https://ads.vk.com/doc/api/info/%D0%A3%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%BE%20API](https://ads.vk.com/doc/api/info/%D0%A3%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%BE%20API)

---

### Устройство API

API реализован в виде набора &laquo;ресурсов&raquo; (объектов предметной области) и &laquo;методов&raquo;
    (операций над ресурсами), что в некоторой степени соответствует REST-идеологии. Основным отличием является то, что
    многие методы позволяют оперировать ресурсами со сложной структурой, включающей в себя другие ресурсы с произвольным
    уровнем вложенности или списки других ресурсов. Многие методы также поддерживают операции над несколькими ресурсами
    одного типа.

Каждый ресурс имеет один или несколько
    типов URL-адресов. Различные операции над ресурсом реализованы в виде различных методов протокола HTTP. Например,
    получение списка рекламных кампаний:

GET /api/v2/ad_plans.json

Создание кампании:

POST /api/v2/ad_plans.json

Получение параметров конкретной кампании:

GET /api/v2/ad_plans/1.json

Для подавляющего большинства методов входные
        и выходные данные представлены в формате JSON. Соответственно, HTTP-запросы и ответы имеют тип application/json.
        Для запросов GET или DELETE, не имеющих тела, тип указывать необязательно.

Для валидации входных и генерации выходных
        данных для каждого ресурса описана одна или несколько структур данных. В описании каждого метода указано, какими
        структурами он оперирует.

Аутентификация

Для аутентификации и авторизации в API
        используется протокол OAuth2. Его реализация описана в отдельной
          статье. Регистрация клиентов для работы с API через OAuth2 пока осуществляется в ручном режиме по заявке в
        Службу поддержки (доступно в интерфейсе сервиса). Как получить доступ к API, описано в инструкции.

Базовые типы данных

API оперирует следующим набором базовых типов
        данных:

  
    
      
        
Тип
                  данных

      
      
        
JSON-представление

      
    
    
      
        
Строка (String)
        

      
      
        
"value"

      
    
    
      
        
Целое число
                (Integer)

      
      
        
"123"

      
    
    
      
        
Десятичная дробь
                (Decimal)

      
      
        
"1.23"

      
    
    
      
        
Булево значение
                (Boolean)

      
      
        
"true" или
                "false"

      
    
    
      
        
Ничего (None)
        

      
      
        
null

      
    
    
      
        
Дата (Date)

      
      
        
"2013-08-18", формат YYYY-MM-DD, если
                явно не указан другой

      
    
    
      
        
Дата и время
                (Datetime)

      
      
        
"2013-08-28 16:49:34", формат
                YYYY-MM-DD HH:MM:SS если явно не указан другой, временная зона Europe/Moscow, если не указана
                другая

      
    
    
      
        
Список (List)
        

      
      
        
["value1", "value2"], элементы списка
                однородны

      
    
    
      
        
Объект (Object)
        

      
      
        
{"id": 1, "name": "Name"}, свойства
                объекта могут быть неоднородны

      
    
  

Сложные типы данных, основанные на базовых,
        описаны в документации по методам и ресурсам.

Базовые ошибки

Ответы с ошибками имеют стандартные статусы
        HTTP-ответов. В теле ответа при этом указана более подробная информация об ошибке в формате JSON (тип
        ответа-ошибки &mdash; application/json).

  
  - 400 &mdash; ошибка валидации структуры данных, присланной в
          запросе;
  
  - 401 &mdash; отсутствие подписи для осуществления аутентификации или же неправильное
          её значение (заголовок Authorization должен содержать корректное значение access_token);
  
  
  - 403 &mdash; операция запрещена для аккаунта, чьим секретным ключом (access_token)
          был подписан запрос;
  
  - 404 &mdash; запрашиваемый ресурс не найден;
  
  - 405 &mdash; ресурс не поддерживает данный HTTP-метод;
  
  - 413 &mdash; тело запроса слишком велико;
  
  - 429 &mdash; превышение лимита на количество запросов в единицу
          времени;
  
  - 500 &mdash; непредвиденная ошибка.

Сжатие ответа

Если ваш клиент поддерживает сжатие, в запросе можно передавать
      заголовок:

Accept-Encoding: gzip, deflate

Лимиты на количество запросов в единицу времени

Сервис ограничивает количество запросов в единицу времени. Ограничения действуют для
      промежутков времени, равных секунде, часу и дню. Ограничения привязаны к календарным периодам
      времени.

Пользовательские лимиты подсчитываются для каждого пользователя независимо. К примеру,
      если в системе существует ограничение в 10 запросов в минуту к определенному методу, то это значит, что каждый
      пользователь может сделать не более 10 запросов в минуту.

Лимиты могут быть настроены по-разному для различных пользователей или групп
      пользователей. Поэтому всегда стоит опираться только на данные, полученнные в реальном времени.

Текущие ограничения возвращаются в HTTP-заголовках ответа на любой запрос (для
      различных методов будут различные значения):

X-RateLimit-RPS-Limit: value &nbsp; &nbsp; # количество запросов в секунду&nbsp;
X-RateLimit-Hourly-Limit: value&nbsp; # количество запросов в час&nbsp;
X-RateLimit-Daily-Limit: value &nbsp; # количество запросов в день

Количество действий до достижения порога также возвращается в HTTP-заголовках
      ответа:

X-RateLimit-RPS-Remaining: value&nbsp; &nbsp; # сколько запросов можно произвести до окончания текущей секунды&nbsp;
X-RateLimit-Hourly-Remaining: value # сколько запросов можно произвести до окончания текущего часа&nbsp;
X-RateLimit-Daily-Remaining: value&nbsp; # сколько запросов можно произвести до окончания текущего дня

Информацию о лимитах для конкретного пользователя также можно
    получить с помощью запроса

  
    
      
        
          
            GET /api/v2/throttling.json
          
        
      
    
  

Ответ содержит текущее значение лимитов, а также количество
    оставшихся запросов по ресурсам, для которых лимиты заданы.

  
    
      
        
          
            {
            &nbsp;&nbsp;&nbsp;&nbsp;"REMARKETINGUSERSLIST": {
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"v2": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"READ": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"remaining": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"60": 1
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limits": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"60": 1
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"CREATE": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"remaining": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"60": 0
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limits": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"60": 0
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"v3": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"READ": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"remaining": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"3600": 200
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limits": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"3600": 200
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"CREATE": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"remaining": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"3600": 10
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limits": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"3600": 10
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"all": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"READ": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"remaining": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"3600": 200
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limits": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"3600": 200
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"CREATE": {
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"remaining": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"60": 1
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"limits": {
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"60": 1
            
            
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
            &nbsp;&nbsp;&nbsp;&nbsp;}
          
        
      
    
  

Для ресурса могут быть заданы как общие лимиты, так и лимиты на
    использование метода определенной версии. Версия соответствует неймспейсу. Так, в приведенном примере c помощью
    метода /api/v2/remarketing/users_lists/&lt;id&gt;.json можно сделать не более одного GET-запроса в минуту, а создать
    новый список нельзя, с помощью /api/v2/remarketing/users_lists/&lt;id&gt;.json можно прочитать информацию по 200
    спискам в час, а создать 10 списков в час. И при этом с помощью запросов любых версий суммарно нельзя прочитать
    информацию по более чем 200 спискам в час, а создавать можно не более 1 списка в час.

После релиза новой версии метода, мы будем постепенно уменьшать
    лимиты использования для предыдущих версии того же самого ресурса.

# Стандарты API

Следующие правила актуальны для всех методов.  

## Параметры запроса

|Название|Формат|Default|Описание|Пример|
|--------|-----|--------|--------|----------|
|fields|\[,\]\*|Зависит от ресурса|Список полей для объекта верхнего уровня|fields=id,name|
|limit|integer|20|Количество объектов в выдаче. Максимум 50|limit=10|
|offset|integer|0|Сдвиг по объектам в выдаче|offset=500|
|sorting|\[-\]?\[,\[-\]?\]\*|-|Сортировка по полям объекта. Список сортируемых полей уникален для каждого ресурса.  - ASC - - DESC|sorting=id,-created|
|\_\_\_|\[,\]\*|-|Фильтры по полям объекта. Список фильтруемых полей уникален для каждого ресурса. Нельзя фильтровать по полям вложенных объектов.|\_id\_\_in=1,2,3 \_status\_\_ne=active \_updated\_\_gt=2018-01-01 00:00:00|
|\_||-|Фильтр на равенство по полю объекта. Правила такие же как в \_\_\_|_id=1|

## Field lookups (стандартные названия)

ne - не равно  
lt - меньше чем  
lte - менее или равно  
gt - более чем  
gte - более или равно   

## Ответ

Коллекция:  
```bash
{ "count": int, // общее число объектов, после применения всех остальных параметров "offset": int, // текущее смещение "limit": int, // количество объектов в выдаче "items": [{ "": field_value, ... }, ...] }
```

Объект:   
```bash
{ "": field_value, ... } 
```