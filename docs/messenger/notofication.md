# Оповещения

## Исполнитель
### Портфолио

#### Уведомление на результат проверки портфолио

Подписаться: action: "subscribe_to_executor_portfolios_for_executor_for_notifications"

Уведомления:

1) Если статус "confirmed"

Пример ответа:

```json
{
  "message": "Your portfolio has been approved",
  "data": {
    "id": 26,
    "type": {
      "id": 6,
      "name": "Тестирование",
      "colour": null,
      "description": null,
      "order": null
    },
    "skills_in_portfolio": [],
    "owner": 3,
    "confirmation": "confirmed",
    "files_in_portfolio": [],
    "date": "2022-02-28T08:36:30.678584Z"
  },
  "action": "create",
  "pk": 26
}
```

2) Если статус "rejected"

Пример ответа:

```json
{
  "message": "Your portfolio has been rejected",
  "data": {
    "id": 26,
    "type": {
      "id": 6,
      "name": "Тестирование",
      "colour": null,
      "description": null,
      "order": null
    },
    "skills_in_portfolio": [],
    "owner": 3,
    "confirmation": "rejected",
    "files_in_portfolio": [],
    "date": "2022-02-28T08:36:30.678584Z"
  },
  "action": "update",
  "pk": 26
}
```
### Правки
#### Уведомления об изменении статуса правки для исполнителя

Подписаться: action: "subscribe_to_order_corrections_for_executor_for_notifications"

Пример ответа:

```json
{
  "message": "New status of edits: wait",
  "data": {
    "id": 1,
    "order_results_for_corrections": [
      {
        "id": 14,
        "files_in_order_result": [
          ...
        ],
        "confirmation": null,
        "comment": "string",
        "order_correction": 1,
        "order": null
      },
      {
        "id": 13,
        "files_in_order_result": [],
        "confirmation": null,
        "comment": "string",
        "order_correction": 1,
        "order": null
      }
    ],
    "files_in_order_corrections": [
      ...
    ],
    "confirmation": "wait",
    "executor_comment": "",
    "customer_comment": "",
    "surcharge": 12,
    "order": 6,
    "this_executor": 1
  },
  "action": "update",
  "pk": 1
}  

```
### Ответы на правки исполнителю
#### Уведомление на результат правки

Подписаться: action: "subscribe_to_executor_portfolios_for_executor_for_notifications"

Уведомления:

1) Если статус "confirmed"


Пример ответа:

```json
{
  "message": "New status of results of edits: accepted",
  "data": {
    "id": 14,
    "files_in_order_result": [
      ...
    ],
    "confirmation": "accepted",
    "comment": "string",
    "order_correction": 1,
    "order": 6
  },
  "action": "update",
  "pk": 14
}
```


#### Уведомления об изменении статуса правки для заказчика

Подписаться: action: "subscribe_to_order_corrections_for_executor_for_notifications"

Пример ответа:

```json
{
  "message": "New status of edits: wait",
  "data": {
    "id": 1,
    "order_results_for_corrections": [
      {
        "id": 14,
        "files_in_order_result": [
          ...
        ],
        "confirmation": null,
        "comment": "string",
        "order_correction": 1,
        "order": null
      },
      {
        "id": 13,
        "files_in_order_result": [],
        "confirmation": null,
        "comment": "string",
        "order_correction": 1,
        "order": null
      }
    ],
    "files_in_order_corrections": [
      ...
    ],
    "confirmation": "wait",
    "executor_comment": "",
    "customer_comment": "",
    "surcharge": 12,
    "order": 6,
    "this_executor": 1
  },
  "action": "update",
  "pk": 1
}  

```
### Ответы на правки заказчику
#### Уведомление на результат правки 

Подписаться: action: "subscribe_to_executor_portfolios_for_executor_for_notifications"

Уведомления:

1) Если статус "confirmed"


Пример ответа:

```json
{
  "message": "New status of results of edits: accepted",
  "data": {
    "id": 14,
    "files_in_order_result": [
      ...
    ],
    "confirmation": "accepted",
    "comment": "string",
    "order_correction": 1,
    "order": 6
  },
  "action": "update",
  "pk": 14
}
```