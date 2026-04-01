# SurveyResultInfoNegative

> Оригинал: [https://ads.vk.com/doc/api/object/SurveyResultInfoNegative](https://ads.vk.com/doc/api/object/SurveyResultInfoNegative)

---

Объект, описывающий информацию для отрицательного последнего экрана опроса (стоп-экрана).

|Field name|Type|Conditions|Description|
|-|-|-|-|
|title|string|`readable``writable``required``max_length=25`|Заголовок последнего экрана анкеты опроса.|
|description|string|`readable``writable``max_length=160` |Сопроводительный текст последнего экрана анкеты опроса.|
|site_url|url|`readable``writable``max_length=2000` |URL внешнего лендинга. В адресе поддерживается [UTM-разметка](https://ads.vk.com/help/articles/utm#tags).|
|condition|[SurveyCondition](../object/SurveyCondition)|`readable``writable``required`|Условие, выполнение которого будет переводить респондента на отрицательный последний экран опроса.|d5:T14d6,