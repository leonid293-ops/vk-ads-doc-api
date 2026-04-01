# SharingKeyUser

> Оригинал: [https://ads.vk.com/doc/api/resource/SharingKeyUser](https://ads.vk.com/doc/api/resource/SharingKeyUser)

---

## /api/v2/sharing_keys/.json

Ресурс, позволяющий активировать и удалять ключи доступа к сторонним источникам данных (спискам пользователей, счётчикам и т.п.). При активации ключа, сегменты им предоставляемые, будут добавлены в список сегментов текущего пользователя. Удалить ключ может только владелец ключа.

Используется объект: [SharingKeyUser](../object/SharingKeyUser)

### POST

Запрос позволяет активировать ключ доступа и добавить себе все или часть источников из него.

Пример запроса:

```HTTP

  POST /api/v2/sharing_keys/abcdefg.json
```

Пример ответа:

```HTTP

	{
	  "id": 200000, 
	  "sources": [
	    {
	      "object_id": 2500000, 
	      "object_type": "users_list", 
	      "params": {
	        "entries_count": 18350, 
	        "id": 2500000, 
	        "name": "Интересы 1", 
	        "type": "vk"
	      }
	    },
	    {
	      "object_id": 1000500, 
	      "object_type": "counter", 
	      "params": {
	        "id": 1000500, 
	        "name": "Мой счетчик" 
	      }
	    }
	  ], 
	  "username": "user@na.me"
	}
```

Используя параметр "sources", можно активировать часть источников из ключа.

Пример запроса с частичной активацией:

```HTTP

  POST /api/v2/sharing_keys/abcdefg.json
  {
  	"sources": {
	      "object_id": 2500000, 
	      "object_type": "users_list"   	
  	}
  }
```

Пример ответа:

```HTTP

	{
	  "id": 200000, 
	  "sources": [
	    {
	      "object_id": 2500000, 
	      "object_type": "users_list", 
	      "params": {
	        "entries_count": 18350, 
	        "id": 2500000, 
	        "name": "Интересы 1", 
	        "type": "vk"
	      }
	    }
	  ], 
	  "username": "user@na.me"
	}
```

Возвращаемые коды статуса:

200 - Ключ успешно активирован.

403 - У пользователя нет доступа к приватному ключу.

404 - В параметре "sources" указан несуществующий источник.

400 - Прочие ошибки.

Примеры ошибок:

```HTTP

	400 Вad Request
	{"error": {"code": "validation_failed", "fields": {  }}}
	- Ошибка в значениях передаваемых данных.

	{"error": {"code": "is_owner", "message": "Cannot activate key for owner"}}
	- Попытка активировать собственный ключ.

	{"error": {"code": "cannot_add_source", "message": "Counter with counter_id 100500 already exists", "arguments": {"source_type": "remarketing_counters",  "source_ids": [100400]}}}
	- Попытка активировать ключ со счетчиком, который уже есть у пользователя. В "source_ids" находятся идентификаторы счетчиков, которые привели к ошибке.

	{"error": {"code": "cannot_add_source", "message": "Counter with counter_id 100500 is not added to account", "arguments": {"source_type": "remarketing_pricelists",  "source_ids": [100600]}}}
	- Попытка активировать ключ с прайс-листом, привязанным к счетчику, если этого счетчика нет у пользователя или в том же ключе. В "source_ids" находятся идентификаторы прайс-листов, которые привели к ошибке.

	403 Forbidden
	{"error": {"code": "access_denied", "message": "Key not available"}}
	- У пользователя нет доступа к приватному ключу.

	404 Not Found
	{"error": {"code": "source_not_found", "message": "Object  with id  not found"}}
	- В параметре "sources" указан несуществующий источник.
```

### DELETE

Запрос позволяет владельцу удалить ключ. При этом у всех пользователей будет отозван доступ к источникам, которые были добавлены по этому ключу. Кампании, в которых использовались эти источники, будут остановлены.

Пример запроса:

```HTTP

  DELETE /api/v2/sharing_keys/abdef.json
```

Возвращаемые коды статуса:

204 - Ключ успешно удален.

404 - Ключ не найден.