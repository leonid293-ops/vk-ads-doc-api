# OrdAgencyActs

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdAgencyActs](https://ads.vk.com/doc/api/resource/OrdAgencyActs)

---

## /api/v2/ord/agency/acts.json
Ресурс для получения списка актов клиентов агентства.

### GET
Возвращает список актов клиентов агентства за указанный месяц. Параметр запроса _month является обязательным.

Дополнительные GET-параметры:

С помощью следующих GET-параметров можно фильтровать данные:

- limit - Количество возвращаемых в ответе клиентов. Значение по умолчанию: 20. Максимальное значение: 50.
- offset - Смещение точки отсчета относительно начала списка клиентов. Значение по умолчанию: 0.
- _month - Месяц отчёта.
- _client__id - Идентификатор клиента.
- _client__id__in - Список идентификаторов клиента через запятую.

Пример запроса с дополнительными параметрами:
``` HTTP
/api/v2/ord/agency/acts.json?limit=50&offset=100$=&_month=2024-10-01&_client_id__in=123,445
```

``` HTTP
{
  "items": [
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
              "inn": "405480305261",
              "phone": "+669635599286",
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
              "inn": "297483315710",
              "phone": "+992659722485",
              "foreign_epayment_method": "string",
              "foreign_registration_number": "string",
              "foreign_inn": "string",
              "foreign_oksm_country_code": "strin"
            },
            "subagent": {
              "name": "string",
              "user_type": "juridical",
              "inn": "4789197592",
              "phone": "+249197306925",
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