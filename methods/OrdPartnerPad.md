# OrdPartnerPad

> Оригинал: [https://ads.vk.com/doc/api/resource/OrdPartnerPad](https://ads.vk.com/doc/api/resource/OrdPartnerPad)

---

## /api/v1/ord/partner/pads/.json

Ресурс, обновлять/редактировать список всех объектов отчётности для всех площадок пользователя рекламного кабинета.

*ВАЖНО* - в конце цепочки обязательно должен быть контрагент с ролью `["publisher"]`.

### POST
#### Запрос редактирует/обновляет объект(ы) отчетности.

##### Пример запроса
```HTTP
   POST /api/v1/ord/partner/pads/777.json

{
    "name": "new_name",  // новое имя ord_partner_pad
    "contracts": [
        {
            "id": 1,  // идентификатор договора который надо обновить
            "contract_number": "new_number",  // новый номер договора
            "contract_date": "2024-06-14",  // новая дата договора
            "contract_subject": "org_distribution",  // новое значение предмета договора
            "vat": true,  // новое значение признака наличия НДС в договоре
            "subagent": {
                "id": 12,  // контрагент которого нужно обновить
                "name": "new subagent name",  // новое имя контрагента 
                "user_type": "foreign_physical",  // новый тип пользователя
                "role": [  // новые роли контрагента
                    "publisher",
                ],
                "inn": "210987654321",
                "foreign_epayment_method": "000000000000',
                "foreign_oksm_country_code": "839"
            }
        }
    ]
}
```

##### Пример ответа:
```HTTP
{
    "items": [
        {
            "id": 777,  // Идентификатор ord_partner_pad
            "url": "https://example.com",  
            "name": "new_name",  // обновленное имя
            "pad_type": "web",
            "contracts": [
                {
                    "id": 1,  // идентификатор договора
                    "level": 1,  // уровень договора
                    "contract_date": "2024-06-14"", 
                    "contract_number": "new_number", 
                    "contract_subject": "org_distribution",  // новый предмет договора
                    "subagent": {
                        "id": 12, 
                        "user_type": "foreign_physical",  
                        "role": [
                            "publisher" // роли контрагента ors / publisher
                        ],
                        "name": "new subagent name",  
                        "inn": "210987654321"
                        "foreign_epayment_method": null,
                        "foreign_oksm_country_code": null,
                        ...
                    },
                    "vat": false 
                }
            ]
        }
    ],
    "count": 1 
}
```

#### Возвращаемые коды статуса:
##### 204 - Данные успешно  изменены.
##### 400 - Ошибка валидации.
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