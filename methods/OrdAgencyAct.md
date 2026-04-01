# OrdAgencyAct

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdAgencyAct](https://ads.vk.com/doc/api/resource/OrdAgencyAct)

---

## /api/v2/ord/agency//acts.json
Ресурс для получения списка актов клиента агентства.

### Доступны GET и POST методы.
### GET
Возвращает список актов клиента агентства за указанный месяц. Параметр запроса _month является обязательным.

Дополнительные GET-параметры:

С помощью следующих GET-параметров можно фильтровать данные:
- _month - Месяц отчёта.

Пример запроса с дополнительными параметрами:
``` HTTP
/api/v2/ord/agency/2147483647/acts.json?_month=2024-10-01
```
2147483647 - id клиента агенства.

``` HTTP
{
  "month": "2024-10-09",
  "client_id": 2147483647,
  "editable": true,
  "status": "uploaded",
  "acts": [
    {
      "serial": "string",
      "vat_included": true,
      "amount": 9999999999.99,
      "amount_total": 9999999999.99,
      "amount_stat": 9999999999.99,
      "errors": [
        "string"
      ],
      "contracts": {
        "client": {
          "contract_number": "string",
          "contract_date": "2024-10-09",
          "contract_type": "mediation",
          "contract_subject": "mediation",
          "name": "string",
          "user_type": "juridical",
          "inn": "2326974262",
          "phone": "+05402488621",
          "foreign_epayment_method": "string",
          "foreign_registration_number": "string",
          "foreign_inn": "string",
          "foreign_oksm_country_code": "strin"
        },
        "agency": {
          "contract_number": "string",
          "contract_date": "2024-10-09",
          "contract_type": "mediation",
          "contract_subject": "mediation",
          "name": "string",
          "user_type": "juridical",
          "inn": "564761988274",
          "phone": "+6088292780094",
          "foreign_epayment_method": "string",
          "foreign_registration_number": "string",
          "foreign_inn": "string",
          "foreign_oksm_country_code": "strin"
        },
        "subagent": {
          "name": "string",
          "user_type": "juridical",
          "inn": "975202613592",
          "phone": "+179904422734",
          "foreign_epayment_method": "string",
          "foreign_registration_number": "string",
          "foreign_inn": "string",
          "foreign_oksm_country_code": "strin"
        }
      },
      "banners": [
        {
          "id": 2147483647,
          "amount": 9999999999.99,
          "amount_stat": 9999999999.99
        }
      ],
      "date_issue": "2024-10-09",
      "date_start": "2024-10-09",
      "date_end": "2024-10-09"
    }
  ]
}
```
### POST

Обновляет, удаляет и добавляет акты клиентов.
        Генерирует исключения API validation_failed, в случае ошибки валидации. 
Каждый раз удаляет все акты клиента за месяц и создаёт новые.

```HTTP
{
  "month": "2024-10-09",
  "acts": [
    {
      "serial": "string",
      "amount": 9999999999.99,
      "amount_total": 9999999999.99,
      "contracts": {
        "client": {
          "contract_number": "string",
          "contract_date": "2024-10-09",
          "contract_type": "mediation",
          "contract_subject": "mediation",
          "name": "string",
          "user_type": "juridical",
          "inn": "47285092194",
          "phone": "+602673356494",
          "foreign_epayment_method": "string",
          "foreign_registration_number": "string",
          "foreign_inn": "string",
          "foreign_oksm_country_code": "strin"
        },
        "agency": {
          "contract_number": "string",
          "contract_date": "2024-10-09",
          "contract_type": "mediation",
          "contract_subject": "mediation",
          "name": "string",
          "user_type": "juridical",
          "inn": "6162189444",
          "phone": "+68186399869025",
          "foreign_epayment_method": "string",
          "foreign_registration_number": "string",
          "foreign_inn": "string",
          "foreign_oksm_country_code": "strin"
        },
        "subagent": {
          "name": "string",
          "user_type": "juridical",
          "inn": "2634231783",
          "phone": "+47178417250",
          "foreign_epayment_method": "string",
          "foreign_registration_number": "string",
          "foreign_inn": "string",
          "foreign_oksm_country_code": "strin"
        }
      },
      "banners": [
        {
          "id": 2147483647,
          "amount": 9999999999.99
        }
      ],
      "date_issue": "2024-10-09",
      "date_start": "2024-10-09",
      "date_end": "2024-10-09"
    }
  ]
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
    "code": "validation_failed",
    "message": "Validation failed",
    "fields": {
      "month": {
        "code": "required",
        "message": "Empty value"
      }
    }
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