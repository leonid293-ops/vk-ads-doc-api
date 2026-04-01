# LeadFormAgreementTemplateDocument

> Оригинал: [https://ads.vk.com/doc/api/object/LeadFormAgreementTemplateDocument](https://ads.vk.com/doc/api/object/LeadFormAgreementTemplateDocument)

---

Объект, описывающий стандартное пользовательское соглашение лид формы.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|company_title|string|`readable``writable``required``max_length=255`|Для физ. лиц: ФИО. Для юр. лиц: юридическое название компании (организации)|
|registration_address|string|`readable``writable``required``max_length=255`|Для физ. лиц: адрес регистрации по месту жительства. Для юр. лиц: юридический адрес компании (организации)|
|email|email|`readable``writable``max_length=255` |Email компании|
|ogrn_or_inn|string|`readable``writable``max_length=32` |ОГРН или ИНН (только для юридических лиц)|c2:T587,Объект, описывающий вариант ответа на вопрос лид формы.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|string|`readable``default_field`|Идентификатор варианта ответа|
|type|integer|`readable``writable``choices =`
  - `0` - Пользовательский вариант ответа
  - `2` - Особый ответ "Ничего из перечисл