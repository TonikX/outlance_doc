# Создание заказа

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