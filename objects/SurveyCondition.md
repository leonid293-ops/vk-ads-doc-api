# SurveyCondition

> Оригинал: [https://ads.vk.com/doc/api/object/SurveyCondition](https://ads.vk.com/doc/api/object/SurveyCondition)

---

Объект условия показа экрана опроса.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|operation_tag|string|`readable``writable``required``choices =`
  - `answer_exists` - Проверка на наличие указанного варианта среди ответов респондента
  - `or` - Объединение вложенных условий логическим ИЛИ|Тег операции/проверки, применяющейся в условии|
|value|object|`readable``writable``required``choices =`
  - [SurveyConditionAnswerExists](../object/SurveyConditionAnswerExists) - Объект условия, использующегося при `operation_tag=answer_exists`
  - [SurveyConditionOr](../object/SurveyConditionOr) - Объект условия, использующегося при `operation_tag=or`|Тип варианта ответа|d2:T8c4,