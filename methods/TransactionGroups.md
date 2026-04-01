# TransactionGroups

> Оригинал: [https://ads.vk.com/doc/api/resource/TransactionGroups](https://ads.vk.com/doc/api/resource/TransactionGroups)

---

## /api/v2/billing/transaction_groups.json

Ресурс позволяет получить данные о группах транзакций пользователя

Используется объект: [TransactionGroup](../object/TransactionGroup)

### GET

Запрос возвращает данные о группах транзакций пользователя

Фильтруемые поля: id, amount, date, first_at, last_at, description, object_id, object_type.

Сортируемые поля: id, amount, date, first_at, last_at, object_id, object_type.

Пример запроса:

```HTTP

   GET /api/v2/billing/transaction_groups.json
```

Пример ответа:

```HTTP

    {
        "count": 2, 
        "limit": 50,
        "offset": 0,
        "items": [
            {
                "amount": "3540.00",
                "client_id": null,
                "date": "2018-11-01",
                "description": "Пополнение счета #3650997 на сумму 3540 RUB (3000 RUB - 540 RUB). Код транзакции: e9c66246278a4e6a85a4c9ba51d33583.",
                "first_at": "2018-11-03 16:24:25",
                "id": 31364364,
                "invoices": [3650997],
                "is_commercial": true,
                "last_at": "2018-11-03 16:24:25",
                "payments_total": "3540",
                "receipt": "https://money.mail.ru/fiscal/get/9ccecf52-6da2-4893-a9d9-47b6f749adfe?format=pdf",
                "tax_amount": "540",
                "type": "deposit",
                "object_id": 0,
                "object_type": "none"
            },
            {
                "amount": "10000.00",
                "client_id": 1234567,
                "date": "2018-11-01",
                "description": "Перевод клиенту",
                "first_at": "2018-11-05 16:24:25",
                "id": 31364381,
                "invoices": [],
                "is_commercial": false,
                "last_at": "2018-11-21 13:12:37",
                "payments_total": "0.00",
                "receipt": null,
                "tax_amount": "0.00",
                "type": "charge",
                "object_id": 0,
                "object_type": "none"
            }
        ]
   }
```