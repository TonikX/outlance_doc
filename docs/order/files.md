# Загрузка файлов в заказ

/api_v2/order/task/file/ [POST]

Необходимо передать поле "file" с файлом и "order" - айди заказа, к которому привязывается файл.

# Загрузка нескольких файлов в результат правки

/api_v2/order_result_/manyfile/ [POST]

Необходимо передать поле "files" с файлом и "order_result" - айди результата правки, к которому привязывается файл.

# Удаление файла результата правки

/api_v2/order_result_/delete/{id}/ [DELETE]

# Загрузка нескольких файлов в правку

/api_v2/order_correction_/manyfile/ [POST]

Необходимо передать поле "files" с файлом и "order_correction" - айди правки, к которому привязывается файл.

# Удаление файла правки

/api_v2/order_correction_/delete/{id}/ [DELETE]

