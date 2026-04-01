# SegmentRelations

> Оригинал: [https://ads.vk.com/doc/api/resource/SegmentRelations](https://ads.vk.com/doc/api/resource/SegmentRelations)

---

## /api/v2/remarketing/segments//relations.json

Ресурс, позволяющий управлять источниками данных, входящими в сегмент аудитории.

Используется объект: [SegmentRelation](../object/SegmentRelation)

### GET

Запрос возвращает информацию об источниках данных в сегменте аудитории.

Пример запроса:

```HTTP

  GET /api/v2/remarketing/segments/243/relations.json?fields=id,object_id,object_type,params
```

Пример ответа:

```HTTP

  {
    "items": [
      {
          "id": 1,
          "object_type": "remarketing_counter",
          "object_id": 23450,
          "params": {"goal_id":"uss", "right":0, "type":"positive", "source_id":2500001, "left":365}
      },
      {
          "id": 2,
          "object_type": "segment",
          "object_id": 481
      }
    ]
  }
```

### POST

Запрос добавляет источники данных в сегмент аудитории.

Пример запроса:

```HTTP

  POST /api/v2/remarketing/segments/243/relations.json
```

```HTTP
  
  {
    "items": [
      {
        "object_type": "remarketing_counter",
        "params": {
          "goal_id": "",
          "right": 0,
          "type": "positive",
          "source_id": 141766795,
          "left": 365
        }
      },
      {
        "object_type": "remarketing_pricelist",
        "params": {
          "source_id": 13,
          "right": 0,
          "type": "positive",
          "left": 365
        }
      },
      {
        "object_type": "remarketing_users_list",
        "params": {
          "source_id": 28612,
          "type": "positive"
        }
      },
      {
        "object_type": "remarketing_lookalike_audience",
        "params": {
          "source_id": 10,
          "reach": 300000,
          "type": "positive"
        }
      },
      {
        "object_type": "remarketing_campaign_list",
        "params": {
          "event_id": 1001,
          "max_count": 2,
          "type": "positive",
          "source_id": 1
        }
      },
      {
        "object_type": "remarketing_group",
        "params": {
          "source_id": 15,
          "type": "positive",
          "source_type": "group"
        }
      },
      {
        "object_type": "remarketing_player",
        "params": {
          "right": 0,
          "type": "positive",
          "left": 365
        }
      },
      {
        "object_type": "remarketing_payer",
        "params": {
          "right": 0,
          "type": "positive",
          "left": 365
        }
      },
      {
        "object_type": "remarketing_game_player",
        "params": {
          "game": "life",
          "right": 0,
          "type": "positive",
          "left": 365
        }
      },
      {
        "object_type": "remarketing_game_payer",
        "params": {
          "game": "life",
          "right": 0,
          "type": "positive",
          "left": 365
        }
      },
      {
        "object_type": "remarketing_vk_group",
        "params": {
          "source_id": 1,
          "type": "positive"
        }
      },
      {
        "object_type": "remarketing_vk_app",
        "params": {
          "type": "positive",
          "source_id": 1
        }
      },
      {
        "object_type": "remarketing_user_geo",
        "params": {
          "type": "positive",
          "source_id": 1
        }
      },
      {
        "object_type": "segment",
        "object_id": 239
      }
    ]
  }

```

Пример ответа:

```HTTP

  {
    "items": [
      {
        "object_type": "remarketing_counter",
        "id": 590,
        "object_id": 116
      },
      {
        "object_type": "remarketing_game_payer",
        "id": 592,
        "object_id": 8
      },
      {
        "object_type": "remarketing_vk_group",
        "id": 593,
        "object_id": 58
      },
      {
        "object_type": "remarketing_player",
        "id": 595,
        "object_id": 8
      },
      {
        "object_type": "remarketing_payer",
        "id": 596,
        "object_id": 10
      },
      {
        "object_type": "remarketing_counter",
        "id": 599,
        "object_id": 117
      },
      {
        "object_type": "remarketing_group",
        "id": 600,
        "object_id": 71
      },
      {
        "object_type": "remarketing_search_phrases",
        "id": 601,
        "object_id": 32
      },
      {
        "object_type": "remarketing_vk_app",
        "id": 603,
        "object_id": 58
      },
      {
        "object_type": "remarketing_campaign_list",
        "id": 604,
        "object_id": 8
      },
      {
        "object_type": "segment",
        "id": 606,
        "object_id": 239
      },
      {
        "object_type": "remarketing_lookalike_audience",
        "id": 607,
        "object_id": 10
      },
      {
        "object_type": "remarketing_game_player",
        "id": 608,
        "object_id": 12
      },
      {
        "object_type": "remarketing_user_geo",
        "id": 610,
        "object_id": 8
      },
      {
        "object_type": "remarketing_users_list",
        "id": 611,
        "object_id": 18
      },
      {
        "object_type": "remarketing_pricelist",
        "id": 612,
        "object_id": 18
      }
    ]
  }
```

Возвращаемые коды статуса:

200 - Источники были успешно добавлены.
400 - Ошибка валидации.

Примеры ошибок:

```HTTP

  {"error": {"code": "validation_failed", "fields": {"pass_condition": {"code": "invalid_condition", "message": "Segment pass condition cannot be greater that number of segment relations"}}}}
  {"error": {"code": "validation_failed", "message": "Validation failed", "fields": {"source_id": {"message": "Unknown {source_type}", "code": "unknown_source", "source_id": 100500}}}}
  {"error": {"code": "validation_failed", "message": "Left should be greater than right"}}
  {"error": {"message": "Relation already exists", "code": "relation_exists"}}
```