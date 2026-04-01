# SurveyQuestion

> Оригинал: [https://ads.vk.com/doc/api/object/SurveyQuestion](https://ads.vk.com/doc/api/object/SurveyQuestion)

---

Объект, описывающий вопрос опроса.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|is_required|boolean |`readable``writable`|Флаг, отвечающий за обязательность заполнения ответа на вопрос респондентом. На текущий момент все вопросы обязательные, так что данный флаг должен быть выставлен в true.|
|text|string|`readable``writable``required``max_length=68`|Текст вопроса|
|type|string|`readable``writable``required``choices =`
  - `one_answer` - Вопрос с возможностью выбора только одного варианта ответа
  - `multiple_answers` - Вопрос с возможностью выбора множества вариантов ответа
  - `text_answer` - Вопрос с текстовым ответом
  - `scale_answer` - Вопрос со шкалой|Тип вопроса|
|answers|list of [Answer](../object/SurveyQuestionAnswer)|`readable``writable``required``max_items=7`|Список вариантов ответа. Для вопросов с `type=text_answer` и `type=scale_answer` указывать варианты ответа не нужно. Для всех остальных типов требуется указывать не менее 2-х вариантов ответа. При этом среди вариантов не должны повторяться особые типы вариантов.|
|scale|[Scale](../object/SurveyQuestionScale) |`readable``writable`|Настройки шкалы. Требуется указывать только в случае `type=scale_answer`.|