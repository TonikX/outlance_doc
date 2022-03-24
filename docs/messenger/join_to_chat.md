## Подключение к чату.

Чат создается автоматически при переводе таблицы OrderReview между заказом заказчика и исполнителем в статус "in_progress".

Подключение к чату.
ws://localhost:8888/messenger/chat/?token={{Обычный ЖВТ токен}}

Формат запросов к чату:

- action: "join_room" - аналог url адреса в http запросах

- pk: "1"

- request_id: 1643788752396 - дата и время (нужно для идентификации запросов сервером) (Пример: request_id = new Date().getTime())

- Далее могут быть любые поля в зависимости от запроса

Во время подключения нужно послать сдедующие запросы:

1) {pk: "1", action: "join_room", request_id: 1643788752396} - подключение к чату.

2) {pk: "1", action: "retrieve", request_id: 1643788752396} - получение **ВСЕХ** сообщений чата по ИД чата (если чат пагинированный action - "retrive_room_paginated_message_action".

Пример ответа:
```json
action: "retrieve" - "Эндпоинт"
data: 
  last_message: {id: 43, created_at_formatted: "31-01-2022 07:54:41",…}
  messages: [{id: 1, created_at_formatted: "25-01-2022 15:08:43",…},…]
pk: 1 - ид чата
errors: []
request_id: 1643788752396 - дата и время (нужно для идентификации запросов сервером
response_status: 200 - код ответа (аналог статусов в хттп)
```

3) {pk: "1", action: "subscribe_to_messages_in_room", request_id: 1643788752396} - подписка на все сообщения из чата

4) {action: "user_chat_list_action", request_id: 1643788752396} - получение всех чатов, к которым подключен юзер (если нужен пагинированный вывод - pag_user_chat_list_action)

Пример ответа:
```json
   action: "user_chat_list_action"
   data:
   0: {pk: 1, executor: {id: 3, username: "moderator1", email: "moderator1@mail.ru"},…}
   1: {pk: 2, executor: {id: 4, username: "moderator2", email: "moderator2@mail.ru"},…}
   errors: []
   request_id: 1643788752396
   response_status: 200
```

5) {pk: "1", message: "", page: "1", action: "retrive_room_paginated_message_action", request_id: 1643788752396} - получение **пагинированного** списка сообщений

Page - номер страницы

Пример ответа:
```json
{
  "page": "1",
  "default_page_size": 30, - количество сообщений поумолчанию
  "page_count_of_messages": 1, - количество сообщений в этом ответе
  "data": [
    {
      "id": 1,
      "created_at_formatted": "25-01-2022 15:08:43",
      "user": {
        "id": 1,
        "username": "testexecutor",
        "email": "testexecutor@outlance.me"
      },
      "text": "dfdfdfdf",
      "date": "2022-01-25T15:08:43.700504Z",
      "chat": 1,
      "reply_to_message": null,
      "read": false
    },
  ]
}
```

6) {message: "", action: "create_message", request_id: 1643788752396} - послать сообщение в чат.

Сообщение приходит автоматически всем участникам чата.

Пример ответа:

```json
{
    "data": {
        "id": 45,
        "created_at_formatted": "02-02-2022 08:21:33",
        "user": {
            "id": 1,
            "username": "testexecutor",
            "email": "testexecutor@outlance.me"
        },
        "text": "",
        "date": "2022-02-02T08:21:33.724162Z",
        "chat": 1,
        "reply_to_message": null,
        "read": false
    },
    "action": "create",
    "pk": 45
}
```

7) {pk: "1", page: "1", action: "pag_user_chat_list_action", request_id: 1643960964254} - пагинированный список чатов ткущего юзера
   action: "pag_user_chat_list_action"
   page: "1"
   pk: "1"
   request_id: 1643960964254

Пример ответа:

```json
{
  "errors": [],
  "data": {
    "page": "1",
    "default_page_size": 30,
    "page_count_of_chats": 2,
    "data": [
      {
        "pk": 1,
        "executor": {
          "id": 3,
          "username": "moderator1",
          "email": "moderator1@mail.ru"
        },
        "customer": {
          "id": 1,
          "username": "testexecutor",
          "email": "testexecutor@outlance.me"
        }
      },
      {
        "pk": 2,
        "executor": {
          "id": 4,
          "username": "moderator2",
          "email": "moderator2@mail.ru"
        },
        "customer": {
          "id": 1,
          "username": "testexecutor",
          "email": "testexecutor@outlance.me"
        }
      }
    ]
  },
  "action": "pag_user_chat_list_action",
  "response_status": 200,
  "request_id": 1643960964254
}
```

6) {"action":"message_read","request_id":1646930383586,"pk":60} - пометить сообщение прочитанным.

pk - идентификатор сообщения.

Пример ответа:

```json
{
   "errors": [],
   "data": {
      "pk": 60
   },
   "action": "message_read",
   "response_status": 200,
   "request_id": 1646930383586
}
```

Кроме того, сработает метод, который вернет сообщение целиком, если Вы подписаны на "subscribe_to_messages_in_room"