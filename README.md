# Petgram

## Содержание
- [1. О сервисе](#1-о-сервисе)
- [2. Функционал](#2-функционал)
- [3. Стек технологий](#3-стек-технологий)
- [4. Установка проекта](#4-установка-проекта)
- [5. Регистрация и авторизация](#5-регистрация-и-авторизация-пользователей)
- [6. Примеры запросов](#6-примеры-запросов)
- [7. Авторы](#7-авторы)

## 1. О сервисе
Сервис предоставляет возможность пользователям делиться своими котиками.
Произведения создаются только администратором сервиса.

## 2. Функционал сервиса
- Реализована система регистрации и аутентификации пользователей
- Авторизованные пользователи могут создавать посты со своими котами, добавляя свои фотографии

## 3. Стек технологий
- Docker
- Nginx
- CI/CD service (GitHub Actions)
### Бекенд
- Python 3.9
- Django
- Django REST FrameWork
- Djoser
- Unit test
- Gunicorn
### Фронтенд
- Javascript
- Node.js
- React


## 4. Установка проекта
- Клонируйте репозиторий
```shell
git clone https://github.com/sqqqwer/kittygram_final.git
```
- Перейдите в проект
```shell
cd kittygram_final/
```
- Запустите docker

(если у вас linux или macOS, то перед docker пишите sudo)
- Запустите проект
```shell
docker compose up -d
```
- Примените миграции
```shell
docker compose exec backend python manage.py migrate
```
- Соберите статические файлы бэкенд приложения
```shell
docker compose exec backend python manage.py collectstatic
```
- Перенесите статические файлы в volume докера
```shell
docker compose exec cp -r /app/collected_static/. /backend_static/static/
```
## 5. Регистрация и авторизация пользователей
### Регистрация
Запрос:
```
POST http://localhost:9000/api/users/
```
```json
{
    "username": "username",
    "password": "admin123456789"
}
```
Ответ:

*Cоздаётся и возвращается новый пользователь*
```json
{
    "email": "",
    "username": "username",
    "id": 1
}
```
### Авторизация
Запрос:
```
POST http://localhost:9000/api/token/login/
```
```json
{
    "username": "username",
    "password": "admin123456789"
}
```
Ответ:

*Возвращает токен*
```json
{
    "auth_token": "5cs81ed89fd6527f9d56c3a9v0ed7847e6f0bdc0"
}
```


## 6. Примеры запросов

### Просмотр первой страницы с постами
Запрос:
```
GET http://localhost:9000/api/cats/?page=1
Authorization: Token 5cs81ed89fd6527f9d56c3a9v0ed7847e6f0bdc0
```
Ответ:

```json
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "name": "кот1",
            "color": "white",
            "birth_year": 2020,
            "achievements": [
                {
                    "id": 1,
                    "achievement_name": "Уронил вазу"
                }
            ],
            "owner": 1,
            "age": 4,
            "image": null,
            "image_url": null
        },
        {
            "id": 2,
            "name": "кот2",
            "color": "white",
            "birth_year": 2021,
            "achievements": [
                {
                    "id": 1,
                    "achievement_name": "Уронил вазу"
                }
            ],
            "owner": 2,
            "age": 3,
            "image": null,
            "image_url": null
        }
    ]
}
```

### Создание котика с достижением
Запрос:
```
POST http://localhost:9000/api/cats/
Authorization: Token 5cs81ed89fd6527f9d56c3a9v0ed7847e6f0bdc0
```
```json
{
    "color": "#FFFFFF",
    "achievements": [
        {
            "achievement_name": "Уронил вазу"
        }
    ],
    "name": "Белый",
    "birth_year": "2020"
}
```
Ответ:

*Cоздаётся и возвращается новый пост с котом*
```json
{
    "id": 1,
    "name": "Белый",
    "color": "white",
    "birth_year": 2020,
    "achievements": [
        {
            "id": 1,
            "achievement_name": "Уронил вазу"
        }
    ],
    "owner": 1,
    "age": 4,
    "image": null,
    "image_url": null
}
```

## 7. Авторы
- _Чернявский Владислав_
- _Команда Яндекс практикума_
