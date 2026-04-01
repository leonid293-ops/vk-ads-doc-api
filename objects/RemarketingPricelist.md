# RemarketingPricelist

> Оригинал: [https://ads.vk.com/doc/api/object/RemarketingPricelist](https://ads.vk.com/doc/api/object/RemarketingPricelist)

---

## API управления прайслистами

API прайслистов предназначено для загрузки списков товаров для динамической рекламы, в том числе для динамического ремаркетинга и привлечения новых пользователей.

Список товаров также называют фидом.

Методы для манипуляции прайслистами:

Просмотр списка своих прайслистов
```
GET /api/v2/remarketing/pricelists.json
```

Загрузка нового прайслиста
```
POST /api/v2/remarketing/pricelists.json
```

Детальный просмотр прайслиста
```
GET /v2/remarketing/pricelists/{id}.json
```

Обновление существующего прайслиста
```
POST /v2/remarketing/pricelists/{id}.json
```

Удаление прайслиста
```
DELETE /v2/remarketing/pricelists/{id}.json
```

### Создание нового прайслиста

Есть несколько типов источников, откуда может быть загружен список товаров.

1. url: прайслист будет скачиваться по указанной ссылке.
Необходимо, чтобы формат данных соответствовал требованиям

Пример запроса для создания такого фида:

```
POST /api/v2/remarketing/pricelists.json
{
  "name": "Мой магазин",
  "status": "active",
  "export_url": "https://user@pass:example.org",
  "remove_utm_tags": true,
  "refresh_period": 720,
  "source_type": "url"
}
```
Значение полей

-   "name": Название прайслиста
-   "status": статус прайслиста.
-   "export_url": ссылка на источник прайслиста со списком товаров. Может содержать данные http-аутентификации.
-   "remove_utm_tags":  указание, что при импорте необходимо удалить utm-ссылки из товаров. 
-   "refresh_period": период обновления в часах. Минимум 1 час
-   "source_type": "url" - тип источника

Чтобы фид загрузился успешно, необходимо учитывать что фид должен быть доступен для скачивания боту.

Бот будет делать запросы с IP-адресов

- 92.242.35.250
- 92.242.34.58

Необходимо внести необходимые разрешения в списках доступа и фаерволах.

Бот будет делать запросы с заголовком  `User-Agent: Rb.Mail.Ru/2.0`

Формат содержимого должен соответствовать одной из спецификаций https://ads.vk.com/help/articles/ecomm_catalog

Фид может быть в архиве(zip или gzip)

Если в export_url будет указана ссылка на сообщество vk, то прайслист будет получен из сообщества вк, на которое будет указывать ссылка

```
POST /api/v2/remarketing/pricelists.json
{
  "name": "Мой магазин",
  "status": "active",
  "export_url": "https://vk.com/club1234567890",
  "remove_utm_tags": true,
  "refresh_period": 720,
  "source_type": "url"
}
```

2. ozon_api, wildberries: Маркетплейсы: товары будут извлечены из маркетплейсов по API.
Поддерживаемые на текущий момент маркетплейсы это Ozon и Wildberries 

Пример для Ozon
```
POST /api/v2/remarketing/pricelists.json
{
  "name": "Мой магазин",
  "status": "active",
  "export_url": "https://www.ozon.ru/seller/a-b-c-123456789/products/?miniapp=seller_123456789",
  "remove_utm_tags": true,
  "refresh_period": 720,
  "source_type": "ozon_api",
  "credentials": {
    "client_id": "string",
    "api_key": "string"
  },
}
```

export_url должен указывать на адрес продавца в ozon.

Обратите внимание, что для запросов в ozon необходимо будет указать client_id и api_key - параметры доступа в кабинет продавца Ozon. Получить их можно в личном кабинете продавца ozon

Пример для Wildberries
```
POST /api/v2/remarketing/pricelists.json
{
  "name": "Мой магазин",
  "status": "active",
  "export_url": "https://www.wildberries.ru/seller/1234567890",
  "remove_utm_tags": true,
  "refresh_period": 720,
  "source_type": "wildberries",
  "credentials": {
    "api_key": "string"
  },
}
```

export_url должен указывать на адрес продавца в Wildberries.

api_key должен содержать ключ доступа в кабинет продавца Wildberries

3. Ручное управление списком товаров

В этом случае export_url не требуется, никаких периодических обновлений списка товаров не будет.

```
POST /api/v2/remarketing/pricelists.json
{
  "name": "Мой магазин",
  "status": "active",
  "remove_utm_tags": true,
  "source_type": "api"
}
```

Создастся прайслист без товаров. Товары можно будет добавлять используя API [OfferBatchTaskDetail](https://ads.vk.com/doc/api/resource/OfferBatchTaskDetail)

---

### Модификация прайслиста

Модифицировать можно параметры, указанные при создании, кроме source_type.

```
POST /v2/remarketing/pricelists/{id}.json
{
  "name": "Ещё один магазин",
  "status": "active",
  "remove_utm_tags": true,
  "export_url": "https://test.ru",
}
```

#### Архивирование прайслиста

status можно изменить в blocked; это будет обозначать, что прайслист архивирован. Все рекламные кампании, к которым привязан этот прайслист, будут остановлены!

Прайслист можно разархивировать в дальнейшем. 

Прайслист, который не используется достаточно продолжительное время(3 дня), архивируется автоматически. Товары фида при выводе из архива необходимо будет обкачать заново.

### Удаление прайслиста

Удаление прайслиста доступно, если все кампании и сегменты к которым привязан прайслист, неактивны 

```
DELETE /v2/remarketing/pricelists/{id}.json
```

эта операция необратима