# Создание проверки портфолио

Проверка создается автоматически во время того, как юзер переводит портфолио из статуса "in_work" в статус "on_check".
В этот момент создаются три таблицы CheckExecutorPortfolio и таблицы CheckSkillInPortfolio, соответствующие скилам портфолио (api_v2.signals.portfolio_review_generator).

/api_v2/portfolio/{id}/ 
### Json Example
```json
{
    "type": 0,
    "categories": [
        0
    ],
    "confirmation": "in_work" -> "on_check" !!!
}
```

# Получение заданий на проверку модераторами

Получение списка доступных для проверки и проверенных портфолио, можно офильтровать по статусу проверки:

Возможные статусы:
- 'confirmed'
- 'not_enough_skills'
- 'no_work'
- 'this_is_spam'
- 'on_check'

Пример с фильтром:

/api_v2/check_portfolio/?page=1&confirmation=no_work [GET]

Пользователь должен быть в группе "moderators"

# Сохранение результатов проверки

Модератор передает список скилов, которые необходимо оценить и результат оценки.
Возможные статусы:
- 'confirmed'
- 'not_enough_skills'
- 'no_work'
- 'this_is_spam'
- 'on_check'

/api_v2/check_portfolio/{id}/ [PATCH]

Пользователь должен быть в группе "moderators", во внешнем ключе на модератора должен быть указан текущий юзер

```json
{
    "check_skills_in_portfolio": [ //список скилов со статусом подтверждения скила
        {
            "id": 0,
            "confirmation": true
        }
    ],
    "confirmation": "confirmed"
}
```

# Проверка результатов

