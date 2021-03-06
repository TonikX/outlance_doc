## Создание заказа

Создание/изменение заказа
/api_v2/order/ [POST/ PATCH]

Статусы заказа:
- 'search'
- 'started'
- 'prepare'
- 'in_progress'
- 'wait_confirm'
- 'completed'
- 'canceled'

Дефолтный статус 'prepare'


### Json Example
```json
{
  "category": [
    0 // ид категорий через запятую (нужно передать список целком)
  ],
  "status": "search", // статус (варианты выше)
  "name": "string",
  "task": "string",
  "price": 0,
  "from_deadline": "2022-01-17T14:10:49.251Z",
  "to_deadline": "2022-01-17T14:10:49.251Z",
  "executor_score": 0,
  "customer_score": 0,
  "term": 0, // срок выполнения
  "type": 0, // ид типа заказа
  "customer": 0 // передавать не нужно, подставится сам
}
```

## Просмотр заказов 

Отобразить только те заказы, которые соответствуют подтвержденным в портфолио категориям categories_filter=true

Нельзя просмотреть заказ целиком, что у юзера нет подтвержденных категорий, которые указаны в заказе.

## Просмотр заказаов в зависимости от роли сейчас

/api_v2/order_for_personal_area/ [GET]

Параметры:

- status - фильтр по статусу заказа 
  /api_v2/order_for_personal_area/?status=prepare[GET]


Для заказчика:
выведутся заказы у которых customer=этот пользователь

Для исполнителя:
выведутся заказы у которых в откликах на заказа (OrderReview), есть отклик у которого status="done" (или 'accepted' или "in_progress")и executor=этот пользователь

