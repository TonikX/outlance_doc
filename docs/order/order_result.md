## Описание таблицы правки к заказу

#### Поля:

- confirmation - статус правки
- executor_comment - коммент к правке от заказчика
- customer_comment - коммент к правке от исполнителя
- surcharge - доплата
- order - внешний ключ на заказ

##### Возможные статусы:

- "wait" - ожидание ответа исполнителя
- "confirmed_by_executor" - исполнитель принял правки в работу
- "not_accepted_by_executor" - исполнитель не принял правки в работу
- "on_check_by_customer" - исполнитель выполнил правки и отправил на проверку заказчику
- "accepted" - заказчик принял правки
- "not_accepted" - заказчик не принял правки, вероятно сделает новое задание на правки

## Создание правок к заказу

Правку может создать только заказчик.
Статус присваивается автоматически.
Статус по уморлчанию "wait" - ожидание ответа исполнителя

Создание: 

[POST] /api_v2/order_correction/

Передать можно только поля: 'customer_comment', 'order'

## Просмотр правок к заказу

Для отображения правок пок конкретному заказу, необходимо послать параметр order со ссылкой на заказ.

Нельзя просмотреть полный список правок на сервере без указания заказа (?order=). При попытке просмотреть все заказы сервер выдаст: "error": "you can't see the list of edits from all orders on the server"

Нельзя просмотреть правки, к заказу, к которому Юзер не имеет отношения.

Пример:

[GET] /api_v2/order_correction/?order=5

**Json Example**
```json
{
  "count": 2,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 1,
      "order_results_for_corrections": [
        {
          "id": 14,
          "files_in_order_result": [
            {
              "id": 2,
              "file": "http://localhost:8888/media/order_result_14/input2_up_21022022_aJWH9GE.xlsx",
              "name": "input2_up_21022022.xlsx",
              "size": 10162352,
              "order_result": 14
            },
            {
              "id": 3,
              "file": "http://localhost:8888/media/order_result_14/input2_up_21022022_2yVSKe7.xlsx",
              "name": "input2_up_21022022.xlsx",
              "size": 10162352,
              "order_result": 14
            }
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
        {
          "id": 1,
          "file": "http://localhost:8888/media/order_correction_1/%D0%93%D0%BE%D0%B2%D0%BE%D1%80%D0%BE%D0%B2_734.pdf",
          "name": "вава",
          "size": null,
          "order_correction": 1
        }
      ],
      "confirmation": "accepted",
      "executor_comment": null,
      "customer_comment": null,
      "surcharge": 12,
      "order": 6
    },
    {
      "id": 2,
      "order_results_for_corrections": [],
      "files_in_order_corrections": [
        {
          "id": 2,
          "file": "http://localhost:8888/media/order_correction_2/input2_up_21022022.xlsx",
          "name": "input2_up_21022022.xlsx",
          "size": 10162352,
          "order_correction": 2
        },
        {
          "id": 3,
          "file": "http://localhost:8888/media/order_correction_2/input2_up_21022022_0nEu4NL.xlsx",
          "name": "input2_up_21022022.xlsx",
          "size": 10162352,
          "order_correction": 2
        }
      ],
      "confirmation": "wait",
      "executor_comment": null,
      "customer_comment": null,
      "surcharge": null,
      "order": 6
    }
  ]
}
```

- order_results_for_corrections - результаты работы по правке
- files_in_order_corrections - файлы в праве

## Ответ на правки со стороны исполнителя

[PATCH] /api_v2/order_correction/{id}

Исполнитель может послать только поля: 'executor_comment', 'surcharge'
Исполнителем должен быть исполнитель именно этого заказа!

**Json Example**
```json
{
  "executor_comment": "string",
  "surcharge": 0
}
```

## Ответ на парвки со стороны заказчика

[PATCH] /api_v2/order_correction/{id}

Заказчик может послать только поля: 'customer_comment', 'confirmation'
Заказчиком должен быть заказчикь именно этого заказа!

**Json Example**
```json
{
  "confirmation": "wait",
  "customer_comment": "string"
}
```

