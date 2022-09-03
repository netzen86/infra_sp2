# Выбираем базовый образ.
FROM python:3.7-slim

# Создаём директорию /app и делаем её рабочей. 
WORKDIR /app

# Копируем файлы проекта в контейнер.
COPY . /app

# Выполняем установку зависимостей внутри контейнера.
RUN apt-get update \
   && apt-get -y install libpq-dev gcc
RUN python3 -m pip install --upgrade pip setuptools
RUN pip3 install -r /app/requirements.txt --no-cache-dir

# Выполнить запуск сервера при старте контейнера.
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]
