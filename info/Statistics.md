# Statistics

> Оригинал: [https://ads.vk.com/doc/api/info/Statistics](https://ads.vk.com/doc/api/info/Statistics)

---

## Статистика v2
API-методы статистики v2 позволяют получать различную статистику по рекламным объектам.

Ограничения и фильтры в этих методах задаются с помощью GET-параметров, а не в теле адреса, как это происходит в API v1.

  - Обработка ошибок

  - Общая статистика

  - Статистика с пагинацией

  - Статистика по целям

  - Статистика по событиям в приложениях

  - Оффлайн конверсии

  - Быстрая статистика

Ограничения запросов

  - Статистика возвращается не более чем за последние 366 дней.&nbsp;

  - В одном запросе можно получить статистику не более чем по 200 объектам.&nbsp;

Обработка ошибок

В случае ошибки возвращается ответ вида:

{
&nbsp; &nbsp; "error":
&nbsp;&nbsp;&nbsp;&nbsp;{
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message":&nbsp;"message_text",
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"code": "CODE"
&nbsp;&nbsp;&nbsp;&nbsp;}
}

Возможные ошибки

HTTP-код
Code
Описание

400
ERR_WRONG_PARAMETER
Некорректное значение параметра, либо не указан обязательный параметр

400
ERR_LIMIT_EXCEEDED
Превышен лимит запрашиваемых дат или количества объектов

400
ERR_WRONG_DATE
Указана некорректная дата

400
ERR_WRONG_BANNERS
Запрашиваемые баннеры не существуют или недоступны для данного API-пользователя

400
ERR_WRONG_ADGROUPS
Запрашиваемые группы не существуют или недоступны для данного API-пользователя

400
ERR_WRONG_ADPLANS
Запрашиваемые рекламные планы не существуют или недоступны для данного API-пользователя

400
ERR_WRONG_USERS
Пользователя не существует или статистика по нему недоступна для данного API-пользователя

403
ERR_ACCESS_DENIED
Нет прав для доступа к API-методу

404
ERR_WRONG_RESOURCE
API-метода не существует

404
ERR_WRONG_IDS
id не существует

500
ERR_INTERNAL
Внутренняя ошибка сервера

503
ERR_INTERNAL
Внутренняя ошибка сервера

&nbsp;

Методы
Общая статистика

GET {host}/api/v2/statistics/{banners|ad_groups|ad_plans|users}/{day|summary}.json

Ресурс возвращает суммарную за все время открутки или подневную за выбранный период статистику по аккаунтам, кампаниям, группам и баннерам.

Ограничения и фильтры задаются с помощью GET-параметров:

Параметр
Формат
Значение по умолчанию
Описание

date_from
YYYY-MM-DD
&nbsp;
Начальная дата. Игнорируется для summary.json.

date_to
YYYY-MM-DD
текущее время
Конечная дата (включительно). Игнорируется для summary.json.

id
Cписок чисел, разделенных запятой, или параметр может быть указан несколько раз с одним аргументом.
&nbsp;
Cписок идентификаторов баннеров, кампании или рекламных планов.

metrics
список текстовых идентификаторов, разделенных запятой
base
Список наборов метрик. Доступные варианты: all, base, events, video, carousel, ad_offers, uniques, uniques_video, tps, romi, playable, custom_event, social_network.

attribution
conversion или impression
conversion
Aтрибуцировать conversion - по времени события, impression - времени показа. Игнорируется для summary.

Все параметры кроме metrics являются обязательными.

В одном запросе можно получить как все статистические метрики, так и конкретные наборы.

#### 1. base - базовые метрики:
* shows - количество показов;
* clicks - количество кликов;
* spent - списания;
* cpm - среднее списание за 1000 просмотров;
* cpc - среднее списание за 1 клик;
* ctr - процентное отношение количества кликов к количеству просмотров;
* vk.goals - количество достижений целей.
* vk.cpa  - среднее списание за достижение 1 цели.
* vk.cr - процентное отношение количества достижений целей к количеству кликов.

#### 2. events - метрики для рекламируемых сообщений в ленте социальных сетей:
* opening_app - количество открытий рекламируемого приложения соцсетей;
* opening_post - количество открытий рекламируемого сообщения в ленте соцсетей;
* moving_into_group - количество переходов на страницу группы из рекламируемого сообщения;
* clicks_on_external_url - количество кликов по внешней ссылке в рекламируемом сообщении;
* launching_video - количество запусков видео в рекламируемом сообщении;
* comments - количество нажатий на кнопку «Комментировать»;
* joinings - количество присоединений к группе через рекламируемое сообщение;
* likes - количество лайков рекламируемого сообщения;
* shares - количество действий "Поделиться" для рекламируемого сообщения;
* votings - количество действий голосования в рекламируемом сообщении.

#### 3. uniques - метрики по количеству уникальных пользователей:
* reach -  устаревшая метрика, ныне отдается всегда 0;
* total - количество уникальных пользователей, увидевших объявления из выбранной кампании от старта рекламной кампании на конец выбранного периода;
* increment - прирост количества уникальных пользователей за выбранный период;
* initial_total - количество уникальных пользователей, увидевших объявления из выбранной кампании от старта рекламной кампании на начало выбранного периода (не включая period_date_start)
* frequency - суточная частота показа объявления за выбранный период.

Примечание: Для рекламных кампаний, у которых пауза в трансляции составила более 90 суток, статистика по уникальным пользователям не будет актуальна.

#### 4. video - метрики для видеорекламы:
* started - количество стартов воспроизведения видео;
* paused - количество пауз воспроизведения видео;
* resumed_after_pause - количество воспроизведения видео после паузы;
* fullscreen_on - количество включений полноэкранного режима воспроизведения видео;
* fullscreen_off - количество выключений полноэкранного режима воспроизведения видео;
* sound_turned_off - количество выключений звука видео;
* sound_turned_on - количество включений звука видео;
* viewed_10_seconds - количество просмотров первых 10 секунд видео;
* viewed_25_percent - количество просмотров первых 25% длительности видео;
* viewed_50_percent - количество просмотров первых 50% длительности видео;
* viewed_75_percent - количество просмотров первых 75% длительности видео;
* viewed_100_percent - количество просмотров 100% длительности видео;
* viewed_10_seconds_rate - процент просмотров с достижением первых 10 секунд видео;
* viewed_25_percent_rate - процент просмотров с достижением первых 25% длительности видео;
* viewed_50_percent_rate - процент просмотров с достижением первых 50% длительности видео;
* viewed_75_percent_rate - процент просмотров с достижением первых 75% длительности видео;
* viewed_100_percent_rate - процент просмотров с достижением 100% длительности видео;
* depth_of_view - средняя глубина просмотра видео (в процентах);
* view_10_seconds_cost - средняя стоимость просмотра первых 10 секунд видео;
* viewed_25_percent_cost - средняя стоимость просмотра первых 25% длительности видео;
* viewed_50_percent_cost - средняя стоимость просмотра первых 50% длительности видео;
* viewed_75_percent_cost - средняя стоимость просмотра первых 75% длительности видео;
* viewed_100_percent_cost - средняя стоимость просмотра 100% длительности видео.

#### 5. carousel - статистика по отдельным слайдам рекламной карусели (N - от 1 до количества слайдов):
* slide_N_shows - количество показов слайда N;
* slide_N_clicks - количество кликов по слайду N;
* slide_N_ctr - процентное отношение количества кликов к количеству просмотров по слайду N;

#### 6. tps - статистика по дополнительным списаниям:
* tps - дополнительные списания за использование сервиса moat;
* tpd - дополнительные списания за использование сторонних данных (от dmp). 

#### 7. playable - метрики Playable Ads: 
* playable_game_open - открытие игры;
* playable_game_close - закрытие игры;
* playable_call_to_action - клики;

#### 8. romi - метрики возврата инвестиций:
* value - заданная ценность события
* romi - показатель возврата инвестиций
* adv_cost_share - доля рекламных расходов

#### 9. uniques_video - уникальные метрики для видеорекламы:
* started - количество уникальных стартов воспроизведения видео;
* viewed_10_seconds - количество уникальных просмотров первых 10 секунд видео;
* viewed_25_percent - количество уникальных просмотров первых 25% длительности видео;
* viewed_50_percent - количество уникальных просмотров первых 50% длительности видео;
* viewed_75_percent - количество уникальных просмотров первых 75% длительности видео;
* viewed_100_percent - количество уникальных просмотров 100% длительности видео;
* viewed_10_seconds_rate - процент уникальных просмотров с достижением первых 10 секунд видео;
* viewed_25_percent_rate - процент уникальных просмотров с достижением первых 25% длительности видео;
* viewed_50_percent_rate - процент уникальных просмотров с достижением первых 50% длительности видео;
* viewed_75_percent_rate - процент уникальных просмотров с достижением первых 75% длительности видео;
* viewed_100_percent_rate - процент уникальных просмотров с достижением 100% длительности видео;
* depth_of_view - средняя глубина уникальных просмотров видео (в процентах);

#### 10. ad_offers - Рекламные оферы:
* offer_postponed - оффер отложен;
* upload_receipt - чек загружен;
* earn_offer_rewards - награда получена;

#### 11. social_network - события социальных сетей:
* vk_subscribe - подписка на пользователя во вконтакте;
* vk_join - вступления в сообщества во вконтакте;
* ok_join - вступления в сообщества в одноклассниках;
* dzen_join - вступления в сообщества в дзене;
* result_join - первое ненулевое значение из vk_subscribe,vk_join,ok_join,dzen_join;
* vk_message - написание сообщений в сообщества вконтакте;
* ok_message - написание сообщений в сообщества одноклассников;
* result_message - первое ненулевое значение из vk_message или ok_message;

Структура ответа:

  - items - массив статистики за запрашиваемый период

  - id - идентификатор объекта

  - rows - массив статистики за конкретную дату

  - date - дата

  - metrics - массивы запрошенных метрик

  - total - суммарная статистика по объекту за запрашиваемый период

  - total - суммарная статистика по всем объектам за запрашиваемый период

Пример запроса:

GET&nbsp;https://ads.vk.com/api/v2/statistics/ad_groups/day.json?id=857683&amp;date_from=2023-12-01&amp;date_to=2023-12-01&amp;metrics=all

{
    "items": [
        {
            "total": {
                "base": {
                    "shows": 0,
                    "clicks": 0,
                    "goals": 0,
                    "spent": "0",
                    "cpm": "0",
                    "cpc": "0",
                    "cpa": "0",
                    "ctr": 0,
                    "cr": 0,
                    "vk": {
                        "goals": 0,
                        "cpa": 0,
                        "cr": 0
                    }
                },
                "events": {
                    "opening_app": 0,
                    "opening_post": 0,
                    "moving_into_group": 0,
                    "clicks_on_external_url": 0,
                    "launching_video": 0,
                    "comments": 0,
                    "joinings": 0,
                    "likes": 0,
                    "shares": 0,
                    "votings": 0,
                    "sending_form": 0
                },
                "uniques": {
                    "reach": 0,
                    "total": 0,
                    "increment": 0,
                    "frequency": 0
                },
                "uniques_video": {
                    "started": 0,
                    "viewed_10_seconds": 0,
                    "viewed_25_percent": 0,
                    "viewed_50_percent": 0,
                    "viewed_75_percent": 0,
                    "viewed_100_percent": 0,
                    "viewed_10_seconds_rate": 0,
                    "viewed_25_percent_rate": 0,
                    "viewed_50_percent_rate": 0,
                    "viewed_75_percent_rate": 0,
                    "viewed_100_percent_rate": 0,
                    "viewed_range_rate": "",
                    "depth_of_view": 0
                },
                "video": {
                    "started": 0,
                    "paused": 0,
                    "resumed_after_pause": 0,
                    "fullscreen_on": 0,
                    "fullscreen_off": 0,
                    "sound_turned_off": 0,
                    "sound_turned_on": 0,
                    "viewed_10_seconds": 0,
                    "viewed_25_percent": 0,
                    "viewed_50_percent": 0,
                    "viewed_75_percent": 0,
                    "viewed_100_percent": 0,
                    "viewed_10_seconds_rate": 0,
                    "viewed_25_percent_rate": 0,
                    "viewed_50_percent_rate": 0,
                    "viewed_75_percent_rate": 0,
                    "viewed_100_percent_rate": 0,
                    "viewed_range_rate": "0",
                    "depth_of_view": 0,
                    "started_cost": "0",
                    "viewed_10_seconds_cost": "0",
                    "viewed_25_percent_cost": "0",
                    "viewed_50_percent_cost": "0",
                    "viewed_75_percent_cost": "0",
                    "viewed_100_percent_cost": "0"
                },
                "carousel": {
                    "slide_1_clicks": 0,
                    "slide_1_shows": 0,
                    "slide_2_clicks": 0,
                    "slide_2_shows": 0,
                    "slide_3_clicks": 0,
                    "slide_3_shows": 0,
                    "slide_4_clicks": 0,
                    "slide_4_shows": 0,
                    "slide_5_clicks": 0,
                    "slide_5_shows": 0,
                    "slide_6_clicks": 0,
                    "slide_6_shows": 0,
                    "slide_1_ctr": 0,
                    "slide_2_ctr": 0,
                    "slide_3_ctr": 0,
                    "slide_4_ctr": 0,
                    "slide_5_ctr": 0,
                    "slide_6_ctr": 0
                },
                "ad_offers": {
                    "offer_postponed": 0,
                    "upload_receipt": 0,
                    "earn_offer_rewards": 0
                },
                "playable": {
                    "playable_game_open": 0,
                    "playable_game_close": 0,
                    "playable_call_to_action": 0
                },
                "tps": {
                    "tps": "0",
                    "tpd": "0"
                },
                "social_network": {
                    "vk_subscribe": 0,
                    "vk_join": 0,
                    "ok_join": 0,
                    "dzen_join": 0,
                    "result_join": 0,
                    "vk_message": 0,
                    "ok_message": 0,
                    "result_message": 0
                },
                "romi": {
                    "value": "0",
                    "romi": 0,
                    "adv_cost_share": 0
                }
            },
            "rows": [
                {
                    "date": "2023-12-01",
                    "base": {
                        "shows": 0,
                        "clicks": 0,
                        "goals": 0,
                        "spent": "0",
                        "cpm": "0",
                        "cpc": "0",
                        "cpa": "0",
                        "ctr": 0,
                        "cr": 0,
                        "vk": {
                            "goals": 0,
                            "cpa": 0,
                            "cr": 0
                        }
                    },
                    "events": {
                        "opening_app": 0,
                        "opening_post": 0,
                        "moving_into_group": 0,
                        "clicks_on_external_url": 0,
                        "launching_video": 0,
                        "comments": 0,
                        "joinings": 0,
                        "likes": 0,
                        "shares": 0,
                        "votings": 0,
                        "sending_form": 0
                    },
                    "uniques": {
                        "reach": 0,
                        "total": 0,
                        "increment": 0,
                        "frequency": 0
                    },
                    "uniques_video": {
                        "started": 0,
                        "viewed_10_seconds": 0,
                        "viewed_25_percent": 0,
                        "viewed_50_percent": 0,
                        "viewed_75_percent": 0,
                        "viewed_100_percent": 0,
                        "viewed_10_seconds_rate": 0,
                        "viewed_25_percent_rate": 0,
                        "viewed_50_percent_rate": 0,
                        "viewed_75_percent_rate": 0,
                        "viewed_100_percent_rate": 0,
                        "viewed_range_rate": "",
                        "depth_of_view": 0
                    },
                    "video": {
                        "started": 0,
                        "paused": 0,
                        "resumed_after_pause": 0,
                        "fullscreen_on": 0,
                        "fullscreen_off": 0,
                        "sound_turned_off": 0,
                        "sound_turned_on": 0,
                        "viewed_10_seconds": 0,
                        "viewed_25_percent": 0,
                        "viewed_50_percent": 0,
                        "viewed_75_percent": 0,
                        "viewed_100_percent": 0,
                        "viewed_10_seconds_rate": 0,
                        "viewed_25_percent_rate": 0,
                        "viewed_50_percent_rate": 0,
                        "viewed_75_percent_rate": 0,
                        "viewed_100_percent_rate": 0,
                        "viewed_range_rate": "0",
                        "depth_of_view": 0,
                        "started_cost": "0",
                        "viewed_10_seconds_cost": "0",
                        "viewed_25_percent_cost": "0",
                        "viewed_50_percent_cost": "0",
                        "viewed_75_percent_cost": "0",
                        "viewed_100_percent_cost": "0"
                    },
                    "carousel": {
                        "slide_1_clicks": 0,
                        "slide_1_shows": 0,
                        "slide_2_clicks": 0,
                        "slide_2_shows": 0,
                        "slide_3_clicks": 0,
                        "slide_3_shows": 0,
                        "slide_4_clicks": 0,
                        "slide_4_shows": 0,
                        "slide_5_clicks": 0,
                        "slide_5_shows": 0,
                        "slide_6_clicks": 0,
                        "slide_6_shows": 0,
                        "slide_1_ctr": 0,
                        "slide_2_ctr": 0,
                        "slide_3_ctr": 0,
                        "slide_4_ctr": 0,
                        "slide_5_ctr": 0,
                        "slide_6_ctr": 0
                    },
                    "ad_offers": {
                        "offer_postponed": 0,
                        "upload_receipt": 0,
                        "earn_offer_rewards": 0
                    },
                    "playable": {
                        "playable_game_open": 0,
                        "playable_game_close": 0,
                        "playable_call_to_action": 0
                    },
                    "tps": {
                        "tps": "0",
                        "tpd": "0"
                    },
                    "social_network": {
                        "vk_subscribe": 0,
                        "vk_join": 0,
                        "ok_join": 0,
                        "dzen_join": 0,
                        "result_join": 0,
                        "vk_message": 0,
                        "ok_message": 0,
                        "result_message": 0
                    },
                    "romi": {
                        "value": "0",
                        "romi": 0,
                        "adv_cost_share": 0
                    }
                }
            ],
            "id": 857683
        }
    ],
    "total": {
        "base": {
            "shows": 0,
            "clicks": 0,
            "goals": 0,
            "spent": "0",
            "cpm": "0",
            "cpc": "0",
            "cpa": "0",
            "ctr": 0,
            "cr": 0,
            "vk": {
                "goals": 0,
                "cpa": 0,
                "cr": 0
            }
        },
        "events": {
            "opening_app": 0,
            "opening_post": 0,
            "moving_into_group": 0,
            "clicks_on_external_url": 0,
            "launching_video": 0,
            "comments": 0,
            "joinings": 0,
            "likes": 0,
            "shares": 0,
            "votings": 0,
            "sending_form": 0
        },
        "uniques_video": {
            "started": 0,
            "viewed_10_seconds": 0,
            "viewed_25_percent": 0,
            "viewed_50_percent": 0,
            "viewed_75_percent": 0,
            "viewed_100_percent": 0,
            "viewed_10_seconds_rate": 0,
            "viewed_25_percent_rate": 0,
            "viewed_50_percent_rate": 0,
            "viewed_75_percent_rate": 0,
            "viewed_100_percent_rate": 0,
            "viewed_range_rate": "",
            "depth_of_view": 0
        },
        "video": {
            "started": 0,
            "paused": 0,
            "resumed_after_pause": 0,
            "fullscreen_on": 0,
            "fullscreen_off": 0,
            "sound_turned_off": 0,
            "sound_turned_on": 0,
            "viewed_10_seconds": 0,
            "viewed_25_percent": 0,
            "viewed_50_percent": 0,
            "viewed_75_percent": 0,
            "viewed_100_percent": 0,
            "viewed_10_seconds_rate": 0,
            "viewed_25_percent_rate": 0,
            "viewed_50_percent_rate": 0,
            "viewed_75_percent_rate": 0,
            "viewed_100_percent_rate": 0,
            "viewed_range_rate": "0",
            "depth_of_view": 0,
            "started_cost": "0",
            "viewed_10_seconds_cost": "0",
            "viewed_25_percent_cost": "0",
            "viewed_50_percent_cost": "0",
            "viewed_75_percent_cost": "0",
            "viewed_100_percent_cost": "0"
        },
        "carousel": {
            "slide_1_clicks": 0,
            "slide_1_shows": 0,
            "slide_2_clicks": 0,
            "slide_2_shows": 0,
            "slide_3_clicks": 0,
            "slide_3_shows": 0,
            "slide_4_clicks": 0,
            "slide_4_shows": 0,
            "slide_5_clicks": 0,
            "slide_5_shows": 0,
            "slide_6_clicks": 0,
            "slide_6_shows": 0,
            "slide_1_ctr": 0,
            "slide_2_ctr": 0,
            "slide_3_ctr": 0,
            "slide_4_ctr": 0,
            "slide_5_ctr": 0,
            "slide_6_ctr": 0
        },
        "ad_offers": {
            "offer_postponed": 0,
            "upload_receipt": 0,
            "earn_offer_rewards": 0
        },
        "playable": {
            "playable_game_open": 0,
            "playable_game_close": 0,
            "playable_call_to_action": 0
        },
        "tps": {
            "tps": "0",
            "tpd": "0"
        },
        "social_network": {
            "vk_subscribe": 0,
            "vk_join": 0,
            "ok_join": 0,
            "dzen_join": 0,
            "result_join": 0,
            "vk_message": 0,
            "ok_message": 0,
            "result_message": 0
        },
        "romi": {
            "value": "0",
            "romi": 0,
            "adv_cost_share": 0
        }
    }
}

Общая статистика с пагинацией

GET {host}/api/v3/statistics/{banners|ad_groups|ad_plans|users}/day.json

Ресурс возвращает суммарную статистику за выбранный период по аккаунтам, кампаниям, баннерам и группам с пагинацией.

Ограничения и фильтры задаются с помощью GET-параметров:

Параметр
Формат
Значение по умолчанию
Описание

date_from
YYYY-MM-DD
&nbsp;
Начальная дата.

date_to
YYYY-MM-DD
Текущая дата
Конечная дата (включительно).

id
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов баннеров, кампаний, групп или пользователей.

id_ne
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов баннеров, кампаний, групп или пользователей с отрицанием.

fields
список запрашиваемых метрик или полей в формате метрика или метрика.название_поля разделенные запятой
base
Список наборов метрик. Доступные метрики: all, base, events, uniques, uniques_video, video, carousel, ad_offers, playable, tps, social_network, romi.

attribution
conversion или impression
conversion
Aтрибуцировать conversion - по времени события, impression - времени показа.

banner_status
список статусов, разделенных запятой. Доступные варианты: all, active, blocked, deleted.
all
Список статусов баннеров, доступен для статистики по кампаниям, группам и баннерам.

banner_status_ne
список статусов, разделенных запятой. Доступные варианты: all, active, blocked, deleted.
&nbsp;
Список статусов баннеров с отрицанием, доступен для статистики по кампаниям, группам и баннерам.

ad_group_status
список статусов, разделенных запятой. Доступные варианты: all, active, blocked, deleted.
all
Список статусов кампаний, групп, доступен для статистики по кампаниям, группам и баннерам.

ad_group_status_ne
список статусов, разделенных запятой. Доступные варианты: all, active, blocked, deleted.
&nbsp;
Список статусов кампаний, групп с отрицанием. Доступен для статистики по кампаниям, группам и баннерам.

ad_group_id
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов групп. Доступен для статистики по баннерам.

ad_group_id_ne
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов групп с отрицанием. Доступен для статистики по баннерам.

package_id
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов пакетов. Доступен для статистики по баннерам.

package_id_ne
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов пакетов с отрицанием. Доступен для статистики по кампаниям, группам и баннерам.

sort_by
поле в формате метрика.название_поля
&nbsp;
Поле по которому будут сортироваться идентификаторы кампаний, групп, баннеров или пользователей. Доступные метрики: base, video, carousel, tps, playable, romi.

d
строковое поле
asc
Направление сортировки. Доступные варианты: asc, desc

limit
целое число от 1 до 250
20
Количество отдаваемых объектов.

offset
целое число
0
Смещение.

Параметр date_from является обязательными.

В одном запросе можно получить как все статистические метрики, так и конкретные наборы.&nbsp;

  - 

  - 
shows - количество показов;

  - 
clicks&nbsp;- количество кликов;

  - 
spent - списания;

  - 
cpm - среднее списание за 1000 просмотров;

  - 
cpc - среднее списание за 1 клик;

  - 
ctr - процентное отношение количества кликов к количеству просмотров;

  - 
vk.goals - количество достижений целей;

  - 
vk.cr - процентное отношение количества достижений целей к количеству кликов;

  - 
vk.cpa - среднее списание за достижение 1 цели.

  - 

  - 
opening_app - количество открытий рекламируемого приложения соцсетей;

  - 
opening_post - количество открытий рекламируемого сообщения в ленте соцсетей;

  - 
moving_into_group - количество переходов на страницу группы из рекламируемого сообщения;

  - 
clicks_on_external_url - количество кликов по внешней ссылке в рекламируемом сообщении;

  - 
launching_video - количество запусков видео в рекламируемом сообщении;

  - 
comments - количество оставленных комментариев в рекламируемом сообщении;

  - 
joinings - количество присоединений к группе через рекламируемое сообщение;

  - 
likes - количество лайков рекламируемого сообщения;

  - 
shares - количество действий "Поделиться" для рекламируемого сообщения;

  - 
votings - количество действий голосования в рекламируемом сообщении.

  - 

  - 
reach - устаревшая метрика, ныне отдается всегда 0;

  - 
total - количество уникальных пользователей, увидевших объявления из выбранной кампании от старта рекламной кампании на конец выбранного периода;

  - 
increment - прирост количества уникальных пользователей за выбранный период;

  - 
initial_total - количество уникальных пользователей, увидевших объявления из выбранной кампании от старта рекламной кампании на начало выбранного периода (не включая period_date_start)

  - 
frequency - суточная частота показа объявления за выбранный период

Примечание: Для рекламных кампаний, у которых пауза в трансляции составила более 90 суток, статистика по уникальным пользователям не будет актуальна.

  - 

  - 
started - количество стартов воспроизведения видео;

  - 
paused - количество пауз воспроизведения видео;

  - 
resumed_after_pause - количество воспроизведения видео после паузы;

  - 
fullscreen_on - количество включений полноэкранного режима воспроизведения видео;

  - 
fullscreen_off - количество выключений полноэкранного режима воспроизведения видео;

  - 
sound_turned_off - количество выключений звука видео;

  - 
sound_turned_on - количество включений звука видео;

  - 
viewed_10_seconds - количество просмотров первых 10 секунд видео;

  - 
viewed_25_percent - количество просмотров первых 25% длительности видео;

  - 
viewed_50_percent - количество просмотров первых 50% длительности видео;

  - 
viewed_75_percent - количество просмотров первых 75% длительности видео;

  - 
viewed_100_percent - количество просмотров 100% длительности видео;

  - 
viewed_10_seconds_rate - процент просмотров с достижением первых 10 секунд видео;

  - 
viewed_25_percent_rate - процент просмотров с достижением первых 25% длительности видео;

  - 
viewed_50_percent_rate - процент просмотров с достижением первых 50% длительности видео;

  - 
viewed_75_percent_rate - процент просмотров с достижением первых 75% длительности видео;

  - 
viewed_100_percent_rate - процент просмотров с достижением 100% длительности видео;

  - 
depth_of_view - средняя глубина просмотра видео (в процентах);

  - 
view_10_seconds_cost - средняя стоимость просмотра первых 10 секунд видео;

  - 
viewed_25_percent_cost - средняя стоимость просмотра первых 25% длительности видео;

  - 
viewed_50_percent_cost - средняя стоимость просмотра первых 50% длительности видео;

  - 
viewed_75_percent_cost - средняя стоимость просмотра первых 75% длительности видео;

  - 
viewed_100_percent_cost - средняя стоимость просмотра&nbsp;100% длительности видео.

  - 

  - 
slide_N_shows - количество показов слайда N;

  - 
slide_N_clicks - количество кликов по слайду N;

  - 
slide_N_ctr - процентное отношение количества кликов к количеству просмотров по слайду N;

  - 

  - 
tps - дополнительные списания за использование сервиса moat;

  - 
tpd - дополнительные списания за использование сторонних данных (от dmp).&nbsp;

  - 

  - 
playable_game_open - открытие игры;

  - 
playable_game_close - закрытие игры;

  - 
playable_call_to_action - клики;

  - 

  - 
value&nbsp;- заданная ценность события

  - 
romi&nbsp;- показатель возврата инвестиций

  - 
adv_cost_share&nbsp;- доля рекламных расходов

  - 

  - 
started&nbsp;- количество уникальных стартов воспроизведения видео;

  - 
viewed_10_seconds&nbsp;- количество уникальных просмотров первых 10 секунд видео;

  - 
viewed_25_percent&nbsp;- количество уникальных просмотров первых 25% длительности видео;

  - 
viewed_50_percent&nbsp;- количество уникальных просмотров первых 50% длительности видео;

  - 
viewed_75_percent&nbsp;- количество уникальных просмотров первых 75% длительности видео;

  - 
viewed_100_percent&nbsp;- количество уникальных просмотров первых 100% длительности видео;

  - 
viewed_10_seconds_rate&nbsp;- процент уникальных просмотров с достижением первых 10 секунд видео;

  - 
viewed_25_percent_rate&nbsp;-  процент уникальных просмотров с достижением первых 25% длительности видео;

  - 
viewed_50_percent_rate&nbsp;-  процент уникальных просмотров с достижением первых 50% длительности видео;

  - 
viewed_75_percent_rate&nbsp;-  процент уникальных просмотров с достижением первых 75% длительности видео;

  - 
viewed_100_percent_rate&nbsp;-  процент уникальных просмотров с достижением первых 100% длительности видео;

  - 
depth_of_view&nbsp;-  средняя глубина уникальных просмотров видео (в процентах);

Структура ответа:

  - items - массив статистики за запрашиваемый период

  - id - идентификатор объекта

  - user_id - идентификатор пользователя, которому принадлежит объект. Доступен для кампаний, групп и баннеров.

  - total - суммарная статистика по объекту за запрашиваемый период

  - total - суммарная статистика по всем объектам за запрашиваемый период

  - limit - ограничение количества отдаваемых объектов

  - offset - смещение

  - count - количество отданных объектов

Пример запроса:

GET&nbsp;https://ads.vk.com/api/v3/statistics/ad_groups/day.json?id=857683&amp;date_from=2021-06-15&amp;date_to=2021-06-16&amp;fields=all&amp;offset=0&amp;limit=20&amp;sort_by=base.clicks&amp;d=asc

{
    "items": [
        {
            "id": 8372481,
            "user_id": 55555,
            "total": {
                "base": {
                    "shows": 75881,
                    "clicks": 270,
                    "goals": 0,
                    "spent": "23328.92",
                    "a_amount": "23328.92",
                    "n_amount": "0",
                    "cpm": "307.44",
                    "cpc": "86.4",
                    "cpa": "0",
                    "ctr": 0.355820297571197,
                    "cr": 0,
                    "vk": {
                        "goals": 0,
                        "cpa": 0,
                        "cr": 0
                    }
                },
                "uniques": {
                    "reach": 0,
                    "total": 786752,
                    "increment": 53327,
                    "initial_total": 105,
                    "frequency": 1.4229377238547078
                    "frequency_total": 17.937582846444224
                },
                "uniques_video": {
                    "started": 2309,
                    "viewed_10_seconds": 1630,
                    "viewed_25_percent": 1587,
                    "viewed_50_percent": 1365,
                    "viewed_75_percent": 1132,
                    "viewed_100_percent": 874,
                    "viewed_10_seconds_rate": 70.59333044608054,
                    "viewed_25_percent_rate": 68.73105240363793,
                    "viewed_50_percent_rate": 59.116500649631874,
                    "viewed_75_percent_rate": 49.02555218709398,
                    "viewed_100_percent_rate": 37.851883932438284,
                    "depth_of_view": 4.227201418729964
                },
                "video": {
                    "started": 80266,
                    "paused": 233,
                    "resumed_after_pause": 68,
                    "fullscreen_on": 13,
                    "fullscreen_off": 21,
                    "sound_turned_off": 11,
                    "sound_turned_on": 22,
                    "viewed_10_seconds": 0,
                    "viewed_25_percent": 33684,
                    "viewed_50_percent": 25182,
                    "viewed_75_percent": 20488,
                    "viewed_100_percent": 18142,
                    "viewed_10_seconds_rate": 0,
                    "viewed_25_percent_rate": 41.965464829442105,
                    "viewed_50_percent_rate": 31.373184162659157,
                    "viewed_75_percent_rate": 25.525128946253705,
                    "viewed_100_percent_rate": 22.602347195574715,
                    "vr": 78.57,
                    "depth_of_view": 32.12134790000132,
                    "viewed_10_seconds_cost": "0",
                    "viewed_25_percent_cost": "0.69",
                    "viewed_50_percent_cost": "0.93",
                    "viewed_75_percent_cost": "1.14",
                    "viewed_100_percent_cost": "1.29"
                },
                "carousel": {
                    "slide_1_clicks": 0,
                    "slide_1_shows": 0,
                    "slide_2_clicks": 0,
                    "slide_2_shows": 0,
                    "slide_3_clicks": 0,
                    "slide_3_shows": 0,
                    "slide_4_clicks": 0,
                    "slide_4_shows": 0,
                    "slide_5_clicks": 0,
                    "slide_5_shows": 0,
                    "slide_6_clicks": 0,
                    "slide_6_shows": 0,
                    "slide_1_ctr": 0,
                    "slide_2_ctr": 0,
                    "slide_3_ctr": 0,
                    "slide_4_ctr": 0,
                    "slide_5_ctr": 0,
                    "slide_6_ctr": 0
                },
                "playable": {
                    "playable_game_open": 67,
                    "playable_game_close": 75,
                    "playable_call_to_action": 24
                },
                "tps": {
                    "tps": "758.81",
                    "tpd": "0"
                },
                "romi": {
                    "value": "2479.5",
                    "romi": 188.5152431929253,
                    "adv_cost_share": 34.66021375277274
                },
                "custom_event": {
                    "custom_event_100": {
                        "alias": "",
                        "count": 0,
                        "cpa": 0,
                        "cr": 0
                    },
                    "custom_event_1116": {
                        "alias": "Transition after reading the article",
                        "count": 1497,
                        "cpa": 0,
                        "cr": 0
                    }
                }
            }
        }
    ],
    "total": {
        "base": {
            "shows": 75881,
            "clicks": 270,
            "goals": 0,
            "spent": "23328.92",
            "a_amount": "23328.92",
            "n_amount": "0",
            "cpm": "307.44",
            "cpc": "86.4",
            "cpa": "0",
            "ctr": 0.355820297571197,
            "cr": 0,
            "vk": {
                "goals": 0,
                "cpa": 0,
                "cr": 0
            }
        },
        "uniques": {
            "reach": 11425,
            "total": 1125,
            "initial_total": 105,
            "increment": 1020,
            "frequency": 8.89287
        },
        "uniques_video": {
            "started": 2309,
            "viewed_10_seconds": 1630,
            "viewed_25_percent": 1587,
            "viewed_50_percent": 1365,
            "viewed_75_percent": 1132,
            "viewed_100_percent": 874,
            "viewed_10_seconds_rate": 70.59333044608054,
            "viewed_25_percent_rate": 68.73105240363793,
            "viewed_50_percent_rate": 59.116500649631874,
            "viewed_75_percent_rate": 49.02555218709398,
            "viewed_100_percent_rate": 37.851883932438284,
            "depth_of_view": 4.227201418729964
        },
        "video": {
            "started": 80266,
            "paused": 233,
            "resumed_after_pause": 68,
            "fullscreen_on": 13,
            "fullscreen_off": 21,
            "sound_turned_off": 11,
            "sound_turned_on": 22,
            "viewed_10_seconds": 0,
            "viewed_25_percent": 33684,
            "viewed_50_percent": 25182,
            "viewed_75_percent": 20488,
            "viewed_100_percent": 18142,
            "viewed_10_seconds_rate": 0,
            "viewed_25_percent_rate": 41.965464829442105,
            "viewed_50_percent_rate": 31.373184162659157,
            "viewed_75_percent_rate": 25.525128946253705,
            "viewed_100_percent_rate": 22.602347195574715,
            "depth_of_view": 32.12134790000132,
            "viewed_10_seconds_cost": "0",
            "viewed_25_percent_cost": "0.69",
            "viewed_50_percent_cost": "0.93",
            "viewed_75_percent_cost": "1.14",
            "viewed_100_percent_cost": "1.29"
        },
        "carousel": {
            "slide_1_clicks": 0,
            "slide_1_shows": 0,
            "slide_2_clicks": 0,
            "slide_2_shows": 0,
            "slide_3_clicks": 0,
            "slide_3_shows": 0,
            "slide_4_clicks": 0,
            "slide_4_shows": 0,
            "slide_5_clicks": 0,
            "slide_5_shows": 0,
            "slide_6_clicks": 0,
            "slide_6_shows": 0,
            "slide_1_ctr": 0,
            "slide_2_ctr": 0,
            "slide_3_ctr": 0,
            "slide_4_ctr": 0,
            "slide_5_ctr": 0,
            "slide_6_ctr": 0
        },
        "playable": {
            "playable_game_open": 67,
            "playable_game_close": 75,
            "playable_call_to_action": 24
        },
        "tps": {
            "tps": "758.81",
            "tpd": "0"
        },
        "romi": {
            "value": "2479.5",
            "romi": 188.5152431929253,
            "adv_cost_share": 34.66021375277274
        },
        "custom_event": {
            "custom_event_100": {
                "alias": "",
                "count": 0,
                "cpa": 0,
                "cr": 0
            },
            "custom_event_1116": {
                "alias": "Transition after reading the article",
                "count": 1497,
                "cpa": 0,
                "cr": 0
            }
        }
    },
    "limit": 20,
    "offset": 0,
    "count": 1
}

Статистика по целям

GET {host}/api/v2/statistics/goals/{banners|ad_groups|ad_plans|users}/day.json

Ресурс возвращает&nbsp;статистику по конверсиям&nbsp;Top@Mail.ru&nbsp;и установкам мобильных приложений&nbsp;по кампаниям, группам и баннерам в разрешении 1 день.&nbsp;

Ограничения и фильтры задаются с помощью GET-параметров:

Параметр
Формат
Значение по умолчанию
Описание

date_from
YYYY-MM-DD
&nbsp;
Начальная дата&nbsp;

date_to
YYYY-MM-DD
текущее время
Конечная дата (включительно)

id
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов баннеров, групп или кампаний

attribution
conversion или impression
conversion
Aтрибуцировать conversion - по времени события, impression - времени показа.

conversion_type
postview; postclick; total; или их комбинации, разделенные через запятую
postclick
Тип конверсии: postclick - постклик, postview - поствью, total - суммарно

Структура ответа:

  - items - массив статистики за запрашиваемый период

  - id - идентификатор объекта

  - rows - массив статистики за конкретную дату

  - date - дата

  - goals - массивы данных статистики по целям

  - conversion_type - тип конверсии

  - source - тип события: topmail - конверсии счётчика, mobile - мобильные конверсии

  - goal - название цели счётчика или тип для мобильных (сейчас только install)

  - counter_id - идентификатор счётчика

  - count - количество конверсий

  - cr - коэффициент конверсии

  - cpa - стоимость одной конверсии

  - value - заданная ценность события

  - romi - показатель возврата инвестиций

  - adv_cost_share - доля рекламных расходов

  - total - суммарная статистика по объекту за весь запрашиваемый период

  - total - суммарная статистика по всем объектам за весь запрашиваемый период

Пример запроса:

GET&nbsp;https://tads.vk.com/api/v2/statistics/goals/banners/day.json?id=1247539,1268343&amp;date_from=2017-09-20&amp;date_to=2017-09-21

{
    "items": [
        {
            "id": 1,
            "rows": [
                {
                    "date": "2017-03-13",
                    "goals": [
                        {
                            "conversion_type": "postclick",
                            "source": "topmail",
                            "goal": "my-goal",
                            "counter_id": 1,
                            "count": 0,
                            "cr": 0.0,
                            "cpa": "0.0",
                            "value": "0",
                            "romi": -100,
                            "adv_cost_share": 0
                        },
                        {
                            "conversion_type": "postclick",
                            "source": "mobile",
                            "goal": "install",
                            "counter_id": 0,
                            "count": 10,
                            "cr": 0.0,
                            "cpa": "0.0",
                            "value": "0",
                            "romi": -100,
                            "adv_cost_share": 0
                        },
                        {
                            "conversion_type": "postview",
                            "source": "mobile",
                            "goal": "install",
                            "counter_id": 0,
                            "count": 5,
                            "cr": 0.0,
                            "cpa": "0.0",
                            "value": "0",
                            "romi": -100,
                            "adv_cost_share": 0
                        },
                        {
                            "conversion_type": "total",
                            "source": "mobile",
                            "goal": "install",
                            "counter_id": 0,
                            "count": 15,
                            "cr": 0.0,
                            "cpa": "0.0",
                            "value": "0",
                            "romi": -100,
                            "adv_cost_share": 0
                        }
                    ]
                }
            ],
            "total": {
                "goals": [
                    {
                        "conversion_type": "postclick",
                        "source": "topmail",
                        "goal": "my-goal",
                        "counter_id": 1,
                        "count": 0,
                        "cr": 0.0,
                        "cpa": "0.0",
                        "value": "0",
                        "romi": -100,
                        "adv_cost_share": 0
                    },
                    {
                        "conversion_type": "postclick",
                        "source": "mobile",
                        "goal": "install",
                        "counter_id": 0,
                        "count": 10,
                        "cr": 0.0,
                        "cpa": "0.0",
                        "value": "0",
                        "romi": -100,
                        "adv_cost_share": 0
                    },
                    {
                        "conversion_type": "postview",
                        "source": "mobile",
                        "goal": "install",
                        "counter_id": 0,
                        "count": 5,
                        "cr": 0.0,
                        "cpa": "0.0",
                        "value": "0",
                        "romi": -100,
                        "adv_cost_share": 0
                    },
                    {
                        "conversion_type": "total",
                        "source": "mobile",
                        "goal": "install",
                        "counter_id": 0,
                        "count": 15,
                        "cr": 0.0,
                        "cpa": "0.0",
                        "value": "0",
                        "romi": -100,
                        "adv_cost_share": 0
                    }
                ]
            }
        }
    ],
    "total": {
        "goals": [
            {
                "conversion_type": "postclick",
                "source": "topmail",
                "goal": "my-goal",
                "counter_id": 1,
                "count": 0,
                "cr": 0.0,
                "cpa": "0.0",
                "value": "0",
                "romi": -100,
                "adv_cost_share": 0
            },
            {
                "conversion_type": "postclick",
                "source": "mobile",
                "goal": "install",
                "counter_id": 0,
                "count": 10,
                "cr": 0.0,
                "cpa": "0.0",
                "value": "0",
                "romi": -100,
                "adv_cost_share": 0
            },
            {
                "conversion_type": "postview",
                "source": "mobile",
                "goal": "install",
                "counter_id": 0,
                "count": 5,
                "cr": 0.0,
                "cpa": "0.0",
                "value": "0",
                "romi": -100,
                "adv_cost_share": 0
            },
            {
                "conversion_type": "total",
                "source": "mobile",
                "goal": "install",
                "counter_id": 0,
                "count": 15,
                "cr": 0.0,
                "cpa": "0.0",
                "value": "0",
                "romi": -100,
                "adv_cost_share": 0
            }
        ]
    }
}

Статистика по событиям внутри приложения

GET {host}/api/v2/statistics/inapp/{banners|ad_groups|ad_plans|users}/day.json

Ресурс возвращает&nbsp;статистику по аттрибуцированным с рекламными показами VK Ads событиями&nbsp;мобильных приложений&nbsp;по кампаниям, группам и баннерам в разрешении 1 день.&nbsp;

Ограничения и фильтры задаются с помощью GET-параметров:

Параметр
Формат
Значение по умолчанию
Описание

date_from
YYYY-MM-DD
&nbsp;
Начальная дата&nbsp;

date_to
YYYY-MM-DD
текущее время
Конечная дата (включительно)

id
список идентификаторов, разделенных запятой
&nbsp;
Список идентификаторов пользователей, баннеров, групп или кампаний

attribution
conversion или impression
conversion
Aтрибуцировать conversion - по времени события, impression - времени показа.

conversion_type
postview, postclick, total или их комбинации, разделенные через запятую
postclick
Тип конверсии:&nbsp;postclick -&nbsp;постклик,&nbsp;postview -&nbsp;поствью,&nbsp;total -&nbsp;суммарно

Структура ответа:

  - items - массив статистики за запрашиваемый период

  - id - идентификатор объекта

  - rows - массив статистики за конкретную дату

  - date - дата

  - inapps - массивы данных статистики по событиям

  - conversion_type

  - cpa - стоимость одной конверсии

  - cr - коэффициент конверсии

  - count - количество конверсий

  - event - название события

  - app - идентификатор мобильного приложения

  - tracker - идентификатор трекера мобильных приложений

  - value - заданная ценность события

  - romi - показатель возврата инвестиций

  - adv_cost_share - доля рекламных расходов

  - total - суммарная статистика по объекту за весь запрашиваемый период

  - total - суммарная статистика по всем объектам за весь запрашиваемый период

Пример запроса:

GET&nbsp;https://ads.vk.com/api/v2/statistics/inapp/ad_groups/day.json?date_from=10.05.2018&amp;date_to=11.05.2018&amp;id=97204343

{
  "total": {
    "inapps": [
      {
        "conversion_type": "postclick",
        "cpa": "256.17",
        "cr": 3.0446194225721785,
        "count": 58,
        "event": "af_add_to_cart",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      },
      {
        "conversion_type": "postclick",
        "cpa": "43.96",
        "cr": 17.74278215223097,
        "count": 338,
        "event": "af_content_view",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      },
      {
        "conversion_type": "postclick",
        "cpa": "4.84",
        "cr": 160.997375328084,
        "count": 3067,
        "event": "af_list_view",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      },
      {
        "conversion_type": "postclick",
        "cpa": "137.57",
        "cr": 5.669291338582677,
        "count": 108,
        "event": "af_view_cart",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      },
      {
        "conversion_type": "postclick",
        "cpa": "7428.97",
        "cr": 0.10498687664041995,
        "count": 6,
        "event": "af_purchase",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      },
      {
        "conversion_type": "postview",
        "cpa": "7428.97",
        "cr": 0.10498687664041995,
        "count": 4,
        "event": "af_purchase",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      },
      {
        "conversion_type": "total",
        "cpa": "7428.97",
        "cr": 0.10498687664041995,
        "count": 10,
        "event": "af_purchase",
        "app": 461,
        "tracker": 1,
        "value": 10.1,
        "romi": 1.1,
        "adv_cost_share": 0.5
      }
    ]
  },
  "items": [
    {
      "total": {
        "inapps": [
          {
            "conversion_type": "postclick",
            "cpa": "256.17",
            "cr": 3.0446194225721785,
            "count": 58,
            "event": "af_add_to_cart",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          },
          {
            "conversion_type": "postclick",
            "cpa": "43.96",
            "cr": 17.74278215223097,
            "count": 338,
            "event": "af_content_view",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          },
          {
            "conversion_type": "postclick",
            "cpa": "4.84",
            "cr": 160.997375328084,
            "count": 3067,
            "event": "af_list_view",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          },
          {
            "conversion_type": "postclick",
            "cpa": "137.57",
            "cr": 5.669291338582677,
            "count": 108,
            "event": "af_view_cart",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          },
          {
            "conversion_type": "postclick",
            "cpa": "7428.97",
            "cr": 0.10498687664041995,
            "count": 2,
            "event": "af_purchase",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          },
          {
            "conversion_type": "postview",
            "cpa": "7428.97",
            "cr": 0.10498687664041995,
            "count": 4,
            "event": "af_purchase",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          },
          {
            "conversion_type": "total",
            "cpa": "7428.97",
            "cr": 0.10498687664041995,
            "count": 10,
            "event": "af_purchase",
            "app": 461,
            "tracker": 1,
            "value": 10.1,
            "romi": 1.1,
            "adv_cost_share": 0.5
          }
        ]
      },
      "rows": [
        {
          "inapps": [],
          "date": "2017-11-21"
        },
        {
          "inapps": [],
          "date": "2017-11-22"
        },
        {
          "inapps": [
            {
              "conversion_type": "postclick",
              "cpa": "124.89",
              "cr": 7.785888077858881,
              "count": 32,
              "event": "af_add_to_cart",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "23.51",
              "cr": 41.3625304136253,
              "count": 170,
              "event": "af_content_view",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "2.26",
              "cr": 430.17031630170317,
              "count": 1768,
              "event": "af_list_view",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "50.59",
              "cr": 19.22141119221411,
              "count": 79,
                "event": "af_view_cart",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            }
          ],
          "date": "2017-11-23"
        },
        {
          "inapps": [
            {
              "conversion_type": "postclick",
              "cpa": "153.79",
              "cr": 6.356968215158925,
              "count": 26,
              "event": "af_add_to_cart",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "23.8",
              "cr": 41.075794621026894,
              "count": 168,
              "event": "af_content_view",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "3.08",
              "cr": 317.6039119804401,
              "count": 1299,
              "event": "af_list_view",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "1999.27",
              "cr": 0.4889975550122249,
              "count": 2,
              "event": "af_purchase",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postview",
              "cpa": "7428.97",
              "cr": 0.10498687664041995,
              "count": 4,
              "event": "af_purchase",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "total",
              "cpa": "7428.97",
              "cr": 0.10498687664041995,
              "count": 10,
              "event": "af_purchase",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            },
            {
              "conversion_type": "postclick",
              "cpa": "137.88",
              "cr": 7.090464547677261,
              "count": 29,
              "event": "af_view_cart",
              "app": 461,
              "tracker": 1,
              "value": 10.1,
              "romi": 1.1,
              "adv_cost_share": 0.5
            }
          ],
          "date": "2017-11-24"
        }
      ],
      "id": 24120913
    }
  ]
}

Оффлайн конверсии

Ресурс возвращает&nbsp;статистику по аттрибуцированным с рекламными показами VK Ads событиями из списков оффлайн конверсий по группам в разрешении 1 день.

GET api/v2/statistics/offline_conversions/{users|ad_groups|ad_plans}/{day|summary}.json

Параметр
Формат
Описание

date_from
YYYY-MM-DD
Начальная дата&nbsp;

date_to
YYYY-MM-DD
Конечная дата (включительно)

id
список идентификаторов, разделенных запятой
Список идентификаторов групп

Фильтры даты учитывают дату события, к которой&nbsp;атрибутирована конверсия

Параметры ответа:

"rate" conversion rate&nbsp;= пользователи, которые сконвертировались и видели РК / все пользователи, видевшие РК
в процентах
"cost" фактическая стоимость привлечения&nbsp;= стоимость РК /&nbsp;пользователи, которые&nbsp;сконвертировались&nbsp;и видели рекламу&nbsp;
"offline" Количество конверсий&nbsp;

Пример запроса:

    GET&nbsp;https://ads.vk.com/api/v2/statistics/offline_conversions/ad_groups/day.json?id=12121212&amp;date_from=2023-09-20&amp;date_to=2023-09-21

{
    "items": [
        {
            "total": {
                "rate": 0,
                "cost": "0",
                "offline": 0
            },
            "rows": [
                {
                    "date": "2023-09-20",
                    "rate": 0,
                    "cost": "0",
                    "offline": 0
                },
                {
                    "date": "2023-09-21",
                    "rate": 0,
                    "cost": "0",
                    "offline": 0
                }
            ],
            "id": 12121212
        }
    ]
}

Быстрая статистика

GET {host}/api/v3/statistics/faststat/{banners|campaigns|ad_plans|users}.json

Ресурс возвращает базовую статистику по рекламным объектам в режиме реального времени, без учёта фильтрации некорректного траффика. Значения в итоговой статистике могут значительно отличаться.&nbsp;

Ограничения и фильтры задаются с помощью GET-параметров:

Параметр
Формат
Описание

id
список идентификаторов, разделенных запятой
Список идентификаторов баннеров, компаний или групп

Все параметры являются обязательными.

Структура ответа:

    
  - last_seen_msg_time - время (в разных форматах) обработки последнего массива статистики.
    
  - 
        banners|campaigns|advertisers|ad_plans - массив поминутной статистики по запрашиваемому объекту:
        
            
  - timestamp - время последнего учтенного события по данному объекту
            
  - 
                minutely - поминутный|суммарный массивы данных статистики по объекту. Для поминутного массива в подмассивах возвращаются значения за последние 60 минут.&nbsp;Последний элемент каждого массива со статистикой соответствует временному интервалу с указанным таймстэмпом:
                
                    
  - clicks - количество кликов;
                    
  - shows - количество показов;
                
            
        
    

Пример запроса:

GET&nbsp;https://ads.vk.com/api/v3/statistics/faststat/ad_plans.json?id=12121212

{
    "last_seen_msg_time": {
        "timestamp": 1707998760,
        "string": "2024-02-15 15:06:00",
        "ago": 48
    },
    "banners": {},
    "campaigns": {},
    "advertisers": {},
    "ad_plans": {
        "12121212": {
            "timestamp": 1707998760,
            "minutely": {
                "clicks": [
                    0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    2, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    0, 0, 5, 0, 0, 0, 0, 0, 0, 0,
                    0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    1, 0, 0, 0, 0, 0, 0, 0, 0, 0
                ],
                "shows": [
                    0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    2, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    0, 0, 5, 0, 0, 0, 0, 0, 0, 0,
                    0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
                    1, 0, 0, 0, 0, 0, 0, 0, 0, 0
                ]
            }
        }
    }
}