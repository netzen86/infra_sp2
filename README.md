# YaMDb

# Проект YaMDb собирает отзывы пользователей на произведения. 

# Технологии

Django 2.2.16
Django REST framework 3.12.4
Gunicorn 20.0.4
Nginx 1.21.3
Postgres 13.0
Docker-compose 1.29.2

## Запуск приложения
В каталоге с проектом создайте файл .env в котором опишите секреты для подключения к БД
```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
```
Для запуска приложения перейдите в каталог infra и выполните команду
```
docker-compose up -d --build                          
```
Для выполнения миграции выполните команду
```
docker-compose exec web python manage.py migrate
````
Для создания пользователя с правами администратора выполните команду
```
docker-compose exec web python manage.py createsuperuser
```
Собрать статические файлы из нескольких приложений в один каталог
```
docker-compose exec web python manage.py collectstatic --no-input 
```
## Регистрации пользователей
- Пользователь отправляет POST-запрос на добавление нового пользователя с параметрами email и username на эндпоинт /api/v1/auth/signup/.
- YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
- Пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).
- При желании пользователь отправляет PATCH-запрос на эндпоинт /api/v1/users/me/ и заполняет поля в своём профайле (описание полей — в документации).
## Описание эндпоинтов и функционала:

Все функции и эндпоинты описаны в документации:
```
http://127.0.0.1/redoc/
```
## Заполнение базы данных

Для заполнения базы данных данными предоставленными с проектом используйте команду 
```
docker-compose exec web python manage.py fill_db
``` 
(с) Супер проект Андрея, Глеба, Димы
