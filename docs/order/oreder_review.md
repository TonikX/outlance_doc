# Связь заказа и исполнителя (Отклик на заказ)

## Создание

Когда текущий юзер обращается к ендпоинту /api_v2/order/{id}/ [GET], для него создается таблица OrderReview (отклик по заказу).

## Обновление отклика на заказ

/api_v2/order/review/{id}/ [PATCH]

Для обновления отклика на заказ необходимо использовать id, полученный при просмотре заказа по ендпоинту
/api_v2/order/{id}/ [GET]

**Пример ответа при просмотре заказа (/api_v2/order/{id}/ [GET]) **
```json
{
  ...
  "customer_score": 0,
  "order_in_order_review": [
    {
      "id": 0, //<------- По данному ID нужно обновлять отклик на заказ по ендпоинту /api_v2/order/review/{id}/ [PATCH]
      "status": "looked",
      "to_price": 0,
      "to_deadline": "2022-01-18T20:33:23.903Z",
      "cancel_reason": "low_budget",
      "show": true
    }
  ],
  "term": 0
}
```

Обновить по ид можно только отклики по заказам, у которых executor=текущий юзер.

Когда status OrderReview имеет одно из следующий значений:** rejected, accepted, in_progress, done - OrderReview заблокирован** для изменений со стороны executor

Статусы исполнителя в заказе:

- looked
- reconciliation
- rejected
- accepted
- in_progress
- done

Причины причины отмены заказа:

- low_budget
- short_time
- incomprehensible_task
- not_enough_skills
- Im_busy

**Json Example**
```json
{
  "status": "looked",
  "cancel_reason": "low_budget",
}
```