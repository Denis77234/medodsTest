# jwtAuth

Api имеет 2 REST пути:

1. /auth/Tokens - обращение через POST, в теле HTTP передавать json с полем GUID, в ответ записывает куки с access и refresh токенами
2. /auth/Refresh - обращение через PUT, с HTTP передавать куки с access и refresh токенами, в ответ обновляет оба токена

## Установка

#### A. Используя Docker
1. Установить образ mongodb
2. Перейти в дерикторию с проектом и прописать в терминал команду $make run

(В случае возникновения ошибок с портами - изменить назначенные по умолчанию порты в Docker-compose)

#### B. Локальная установка
1. Скачать mongodb
2. Установить 4 переменные окружения MONGO_URI - uri для подключения в базе данных, <br>
ACC_SECRET - ключ шифрования access токена, REF_SECRET - ключ шифрования refresh токена,<br>
JWTSERV_PORT - порт по которому будет производиться обращение к серверу
3. Перейти в дерикторию с проектом и прописать в терминал команду $make runLocal



## Задание

Используемые технологии:

Go
JWT
MongoDB

Задание:

Написать часть сервиса аутентификации.

Два REST маршрута:

Первый маршрут выдает пару Access, Refresh токенов для пользователя сидентификатором (GUID) указанным в параметре запроса

Второй маршрут выполняет Refresh операцию на пару Access, Refreshтокенов

Требования:

Access токен тип JWT, алгоритм SHA512, хранить в базе строго запрещено.

Refresh токен тип произвольный, формат передачи base64, хранится в базеисключительно в виде bcrypt хеша, должен быть защищен от изменения настороне клиента и попыток повторного использования.

Access, Refresh токены обоюдно связаны, Refresh операцию для Access токена можно выполнить только тем Refresh токеном который был выдан вместе с ним.