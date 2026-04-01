# LeadForm

> Оригинал: [https://ads.vk.com/doc/api/object/LeadForm](https://ads.vk.com/doc/api/object/LeadForm)

---

Ресурс для создания/модификации лид формы.

|Field name|Type|Conditions|Description|
|-|-|-|-|
|id|string|`readable``default_field`|Идентификатор формы|
|name|string|`readable``writable``required``max_length=255`|Название формы|
|status|integer|`readable``writable``choices =`
  - `1` - Активная
  - `2` - В архиве|Статус формы. Перевод активной формы в архив и обратно выполняется только специльными запросами. Для форм в архиве недоступно обновление|
|created|datetime|`readable`|Время создания|
|updated|datetime|`readable`|Время последнего обновления|
|leads_count|integer|`readable`|Количество лидов, собранных формой|
|ad_plans_count|integer|`readable`|Количество рекламных кампаний, в которых используется форма|
|ad_plan_ids|list of uint32|`readable`|Идентификаторы рекламных кампаний, в которых используется форма|
|ad_group_ids|list of uint32|`readable`|Идентификаторы рекламных групп, в которых используется форма|
|banner_ids|list of uint32|`readable`|Идентификаторы рекламных объявлений, в которых используется форма|
|active_ad_plan_ids|list of uint32|`readable`|Идентификаторы активных рекламных кампаний, в которых используется форма|
|first_screen_type|string|`readable``writable``required``choices =`
  - `compact` - компактный тип
  - `long_text` - длинное описание
  - `award` - информация о награде за прохождение формы|Тип приветственной части, которую пользователь видит сразу при открытии формы|
|title|string|`readable``writable``required``max_length=50`|Заголовок формы|
|description|string|`readable``writable``max_length=35`|Описание формы. Отображается и при этом обязательно только при `first_screen_type=compact`|
|long_description|string|`readable``writable``max_length=350`|Длинное описание формы. Отображается и при этом обязательно только при `first_screen_type=long_text`. Максимальное количество переносов строки подряд - 2|
|company_title|string|`readable``writable``required``max_length=30`|Название компании|
|logo_id|string|`writeable``required`|Идентификатор логотипа компании, выдается при загрузе логотипа|
|logo|object|`readable`|Логотип компании|
|award|[Award](../object/LeadFormAward)|`readable``writeable`|Награда за прохождение формы. Отображается и при этом обязательна только при `first_screen_type=award`|
|gradient|integer|`readable``writable``choices =`
  - `0` - #FF7583 0%, #E62E40 100%
  - `1` - #FF80D5 0%, #E645B1 100%
  - `2` - #FFD54F 0%, #E7A902 100%
  - `3` - #6CD97E 0%, #12B312 100%
  - `4` - #8AE6E6 0%, #12B3B3 100%
  - `5` - #73D0FF 0%, #3885E1 100%
  - `6` - #FF4D87 0%, #9F40FF 100%
  - `100` - цвет по умолчанию
  - `101` - цвет берётся из `main_color`|Цвет фона формы. Значения с 0 по 6 представляют собой градиенты|
|contact_fields|list of string|`readable``writable``required` `choices =`
  - `first_name` - Имя
  - `email` - Почтовый адрес
  - `phone` - Номер телефона
  - `birth_date` - Дата рождения
  - `city` - Город
  - `social_media_profile` - Ссылка на страницу в социальной сети|Контактные данные, собираемые после ответа на вопросы формы|
|result_info|[ResultInfo](../object/LeadFormResultInfo)|`readable``writeable``required`|Информация для последнего экрана формы|
|agreement|[Agreement](../object/LeadFormAgreement)|`readable``writeable``required`|Пользовательское соглашение формы|
|notifications|list of [Notification](../object/LeadFormNotification)|`readable``writeable`|Настройки уведомлений формы|
|pages|list of [Page](../object/LeadFormPage)|`readable``writeable``max_items=1`|Список страниц формы. Если страницы не указаны, то при заполнении формы пользователь сразу перейдет к вводу контактных данных|
|required_answers|boolean|`readable``writable`|Флаг обязательности вопросов|
|main_color|string|`readable``writable`|Основной цвет формы в HEX формате (пример: #FFFAAA)|
|main_image_id|string|`writeable`|Идентификатор обложки формы, выдается при загрузе обложки|
|main_image|object|`readable`|Обложка формы|