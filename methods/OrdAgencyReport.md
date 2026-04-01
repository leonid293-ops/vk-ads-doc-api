# OrdAgencyReport

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdAgencyReport](https://ads.vk.com/doc/api/resource/OrdAgencyReport)

---

## /api/v2/ord/agency/report.json
Ресурс обобщенных ОРД данных клиентов агентства об их актах. Параметр запроса _month является обязательным.

## GET

Дополнительные GET-параметры:

С помощью следующих GET-параметров можно фильтровать данные:

- limit - Количество возвращаемых в ответе клиентов. Значение по умолчанию: 20. Максимальное значение: 50.
- offset - Смещение точки отсчета относительно начала списка клиентов. Значение по умолчанию: 0.
- _month - Месяц отчёта.
- _q - полнотекстовый поиск по 'client_id', 'client_name', 'original_contract_info__name', 'agency_contract_info__name'.

С помощь параметра sorting доступна сортировка по полям 'client_id', 'client_name', 'direct', 'original_contract_info__name', 'agency_contract_info__name', 'amount'.

Пример запроса с дополнительными параметрами:
``` HTTP
/api/v2/ord/agency/report.json?limit=50&offset=100$=&_month=2024-10-01&_q=2147483647&sorting=

```HTTP
{
  "items": [
    {
      "month": "2024-10-09",
      "client_id": 2147483647,
      "client_name": "string",
      "direct": true,
      "editable": true,
      "acts": 4294967295,
      "amount": 0,
      "amount_stat": 0,
      "original_contract_info": {
        "name": "string",
        "inn": "string",
        "contractor_inn": "string",
        "contractor_name": "string"
      },
      "agency_contract_info": {
        "name": "string",
        "inn": "string",
        "contract_number": "string"
      },
      "act_status": "unfilled"
    }
  ]
}
```

Возвращаемые коды статуса:

200 - Клиент был успешно добавлен.

400 - В следующих случаях:

- Ошибка сортировки multiple_sorting_fields

404 - Клиент с указанным ID не существует.

Примеры ошибок:

```HTTP

{"error": {"code": "multiple_sorting_fields", "message": "Sorting by multiple fields is not supported"}}
- Сортировка по нескольким полям не поддерживается.
```