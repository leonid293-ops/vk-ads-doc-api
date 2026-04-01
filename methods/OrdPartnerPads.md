# OrdPartnerPads

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdPartnerPads](https://ads.vk.com/doc/api/resource/OrdPartnerPads)

---

## /api/v1/ord/partner/pads.json

Ресурс, получить список всех объектов отчётности для всех указанной площадки пользователя рекламного кабинета.

*ВАЖНО* - в конце цепочки обязательно должен быть контрагент с ролью 
 `["publisher"]`.

### GET

#### Запрос возвращает список всех объектов отчётности.

##### Пример запроса:

```HTTP

   GET /api/v1/ord/partner/pads.json
```

##### Пример ответа:

```HTTP
{
    "count": 2,
    "items": [
      {
        "id": 1,  // Идентификатор ord_partner_pad
        "url": "https://vk.com",
        "name": "ВКонтакте",
        "contracts": [
          {
            "id": 1,  // идентификатор договора
            "subagent": {
              "id": 225,  // идентификатор контрагента
              "inn": "123456789012",
              "name": "ИП Васька Петька Ванька",
              "phone": "+70000000000",
              "role": [
                  "publisher",
                  "ors"
              ],
             "site": "https://new.site.com",
             "user_type": "ip",
              "foreign_epayment_method": null,
              "foreign_oksm_country_code": null,
              "foreign_registration_number": null
             }
            },
            "level": 1,
            "contract_date": "2023-01-01",
            "contract_number": "Договор №1 от 2023-01-01",
            "contract_subject": "distribution",
            "vat": true
          },
          {
            "id": 2,
            "subagent": {
              "id": "2",
              "user_type": "ip",
              "roles": ["publisher"],
              "name": "ИП Другой",
              "inn": "123456789012",
              ...
            },
            "level": 2,
            "contract_date": "2023-01-01",
            "contract_number": "Договор №1 от 2023-01-01",
            "contract_subject": "distribution",
            "vat": false
          },
        ]
      }
    ]
}
```

#### Ресурс поддерживает постраничный вывод с помощью параметров limit, offset

##### limit - количество объектов в ответе. (По умолчанию 20)

```HTTP

    GET /api/v1/ord/partner/subagents.json?limit=10
```

##### offset - смещение на N объектов от начала текущей выборки

```HTTP

    GET /api/v1/ord/partner/subagents.json?limit=10&offset=10
```

#### Возвращаемые коды статуса:

##### 200 - Данные успешно получены.

##### 403 - Ошибка доступа.

Примеры ошибок: 

1) Пользователь не является ОРД юзером:

```HTTP
    {
        "error": {
            "message": "Access denied",
            "code": "access_denied",
            "required_permission": "can_use_partner_ord_api"
        }
    }
```