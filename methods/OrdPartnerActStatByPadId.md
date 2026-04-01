# OrdPartnerActStatByPadId

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdPartnerActStatByPadId](https://ads.vk.com/doc/api/resource/OrdPartnerActStatByPadId)

---

## /api/v1/ord/partner/acts//.json

Ресурс, для 
просмотра/создания/редактирования цепочки актов (заполнение сумм и дат), и получаения списка актов (по договорам) для указанной площадки  владельца кабинета за указанный период.

*ВАЖНО* - создавать/изменять цепочку актов можно только до *20-ого* числа текущего месяца

#### Описание полей:

##### *month* - всегда должен указываться в формате: `YYYY-MM-01 (2024-01-01, 2023-11-01 и т.д.)`

##### *ord_pad_id* - id площадки, можно получить из API OrdPartnerPad или OrdPartnerPads

### GET

#### Запрос возвращает статистику по актам за указанный месяц для конкретной площадки.

##### Пример запроса:

```HTTP
   GET /api/v1/ord/partner/acts/2024-07-01/777.json
```

##### Пример ответа:

```HTTP
{
"acts_count": 4,
"contracts_count": 4,
"id": 777,
"name": "Почта",
"total_amount": "258337.38",
"url": "http://longo.mailos.ru"
}
```

#### Запрос возвращает цепочку актов и контрактов за указанный месяц для конкретной площадки.

##### Пример запроса:

```HTTP
   GET /api/v1/ord/partner/acts/2024-07-01/42.json?fields=id,url,name,total_amount,contracts,acts
```

##### Пример ответа:

```HTTP
{
  "count": 1,
  "items": [
    {
      "acts": [
        {
          "act_date": "2024-05-01",
          "amount": "1.00",
          "has_vat": false,
          "id": 74,
          "ord_contract_id": 286
        },
        {
          "act_date": "2024-05-29",
          "amount": "345.00",
          "has_vat": false,
          "id": 75,
          "ord_contract_id": 287
        }
      ],
      "contracts": [
        {
          "contract_number": "111",
          "id": 286,
          "level": 1,
          "subagent": {
            "foreign_epayment_method": null,
            "foreign_registration_number": null,
            "id": 56,
            "inn": "0000000000",
            "name": "ОРС создан в форме"
          }
        },
        {
          "contract_number": "11",
          "id": 287,
          "level": 2,
          "subagent": {
            "foreign_epayment_method": null,
            "foreign_registration_number": null,
            "id": 49,
            "inn": "000000000000",
            "name": "ИП РС №1"
          }
        }
      ],
      "id": 42,
      "name": "FORTESTINGAPP: SITE",
      "total_amount": "17.50",
      "url": "http://viadata.store"
    }
  ]
}
```

### POST
#### Запрос создает/обновляет цепочку актов для указанной площадки.

##### Пример запроса:
```HTTP
   POST /api/v1/ord/partner/acts/2024-07-01/42.json

{
  "acts": [
    {
      "contract_id": 1,
      "act_date": "2023-12-14",
      "amount": "300.321",
      "has_vat": false,
    },
    {
      "contract_id": 2,
      "act_date": "2023-12-14",
      "amount": "200",
      "has_vat": true,
    }
  ]
}
```

##### Пример ответа:
```HTTP
{
  "acts_count": 2,
  "contracts_count": 2,
  "id": 42,
  "name": "test ord partner pad",
  "total_amount": "500.321",
  "url": "https://vk.ru"
}
```

#### Возвращаемые коды статуса:

##### 204 - Данные успешно изменены.
##### 400 - Ошибка валидации.

#### Примеры ошибок: 

1) Ошибки в формате данных (пустое значение, больше/меньше допустимого значения и т.д.):

```HTTP

    {
        "error": {
            "fields": {
                "description": {
                    "message": "Empty value",
                    "code": "required"
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```

2) Ошибки при попытке создания/изменения цепочки в случае если дата(в которую происходит запрос) превышает 20-ое число месяца:

```HTTP
    {
        "error": {
            "fields": {
                "description": {
                    "message": "Bad date: valid only before the 20 day of the month",
                    "code": "bad_date"
                }
            },
            "message": "Validation failed",
            "code": "validation_failed"
        }
    }
```