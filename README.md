# Лабораторная работа №10

- [Лабораторная работа №10](#лабораторная-работа-10)
    - [Инструкции по запуску проекта](#инструкции-по-запуску-проекта)
    - [Задания](#задания)
    - [Примеры использования](#примеры-использования)
    - [Список использованных источников](#список-использованных-источников)

## Инструкции по запуску проекта
1) Склонируйте репозиторий с проектом: git clone [https://github.com/2Vladimir2/lab_10_php.git](https://github.com/2Vladimir2/lab_10_php.git).
2) Запустите веб-сервер: php -S localhost:80.
3) Откройте браузер и перейдите по адресу http://localhost для доступа к заданию.

## Задания
__Задание 1.__ Создайте базу данных “event_platform”.

__Задание 2.__ Создайте следующие таблицы в базе данных и корректно установите между
ними отношения.

2.1. Структура таблицы `users`: пользователи

1. `id` (integer) — primary key
2. `name`
3. `surname`
4. `email` — unique key

2.2. Структура таблицы `events`: мероприятия

1. `id`
2. `name`: название мероприятия
3. `price`: цена мероприятия
4. `number_seats`: количество мест
5. `date`: дата и время

2.3. Структура таблицы `event_records`: записи на мероприятие

1. `id`
2. `user_id`: id пользователя
3. `event_id`: id мероприятия

2.4. Структура таблицы `roles`: роли (user / manager)

1. `id`
2. `name`: название роли


__Задание 3.__ Внесите изменения в таблицу пользователей, добавив поле role_id,
содержащее идентификатор определенной роли.

__Задание 4.__ Создайте четыре страницы:

- Страница с текущими мероприятиями
- Страница для записи на определенное мероприятие
- Регистрация
- Авторизация

__Задание 5.__ Разработайте административную панель (доступную только пользователю с
ID 'manager'), обладающую следующим функционалом:

- Добавление и изменение мероприятия
- Просмотр зарегистрированных на мероприятие.


__Задание 6.__ Сохраняйте все необходимые данные в базе данных.

## Дополнительные задания

__Задание 7 (1 уровень сложности).__ Создайте более сложную схему ролей.

| Таблица `roles` | Таблица `capabilities` | Таблица `roles_capabilities` |
|----------|----------|----------|
| Содержит список ролей, например,  | Описывает возможности ролей, например,  | Связывает роли с их возможностями, определяя, какие возможности доступны для каждой роли.   |
| - user| - can_view_panel          | - `id`        |
| - manager         | - can_edit_event          | - `role_id`      |
| - `id`            | - `id`          | - `capability_id`        |
| - `name` — название роли        | - `name` — название возможности          |

__Задание 8 (2 уровень сложности).__ Реализуйте систему аутентификации на основе
токенов. В таблице users добавьте поле token, которое будет использоваться для
хранения токенов пользователей: 

1. Когда пользователь входит в систему (например, вводит логин и пароль), сервер
проверяет его учетные данные. Если они верны, сервер создает уникальный токен
доступа.
2. Клиент сохраняет полученный токен, обычно в localStorage или cookies браузера,
чтобы иметь доступ к нему на протяжении сеанса работы.
3. Каждый раз, когда клиент отправляет запрос к защищенным ресурсам сервера, он
должен включать токен в заголовке запроса или в другом безопасном месте.
4. Сервер получает запрос и проверяет переданный токен. Он проверяет, действителен
ли токен и имеет ли он права доступа к запрашиваемому ресурсу.


## Примеры использования

```sql
// Задание 2. Создание таблиц
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    surname VARCHAR(255),
    email VARCHAR(255) UNIQUE
);

CREATE TABLE events (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    price DECIMAL(10, 2),
    number_seats INT,
    date DATETIME
);

CREATE TABLE event_records (
    id INT PRIMARY KEY,
    user_id INT,
    event_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (event_id) REFERENCES events(id)
);

CREATE TABLE roles (
    id INT PRIMARY KEY,
    name VARCHAR(255)
);

// Задание 3. Добавление поля role_id в таблицу users
ALTER TABLE users ADD COLUMN role_id INT;
ALTER TABLE users ADD FOREIGN KEY (role_id) REFERENCES roles(id);

// Задание 8. Реализация системы аутентификации на основе токенов
ALTER TABLE users ADD COLUMN token VARCHAR(255);
```
__Задание 4.__ Создайте четыре страницы:

- Страница с текущими мероприятиями

<img width="1011" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/0dd4bd66-252b-4b16-adcb-1d85de9c8efb">


- Страница для записи на определенное мероприятие

<img width="794" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/39d88f6f-a1a9-4376-a769-ef32b65c3450">


- Регистрация

<img width="662" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/3f5b01f5-fcfe-4647-9710-70d87d969aa7">



- Авторизация

<img width="670" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/502a8dd0-b37f-4664-a376-f31be2736549">


__Задание 5.__ Разработайте административную панель (доступную только пользователю с
ID 'manager'), обладающую следующим функционалом:

<img width="905" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/b72ad5d5-c933-4baa-8cc9-e8ba4cbbd743">


- Добавление и изменение мероприятия

<img width="613" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/ca7a6600-3138-4f62-baf2-0418f9660332">
<img width="617" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/bf14e607-8054-4d19-a37d-172760cc8382">



- Просмотр зарегистрированных на мероприятие.

<img width="563" alt="image" src="https://github.com/2Vladimir2/lab_10_php/assets/159247721/4253b903-1c85-41f9-a908-aea11f3755c3">


__Задание 8 (2 уровень сложности).__ Реализуйте систему аутентификации на основе
токенов. 

Пример:
```php
// Проверка, авторизован ли пользователь
if (!isset($_COOKIE['token'])) {
    // Перенаправление на страницу авторизации
    header("Location: /autorisation.php");
    exit;
}

```

## Список использованных источников

https://www.php.net/manual/ru/book.pdo.php

https://www.php.net/manual/ru/reserved.variables.cookies

https://www.php.net/manual/ru/function.password-hash
