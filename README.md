![Build Status](https://github.com/xdan/jodit/workflows/Run%20tests/badge.svg)](https://github.com/norugin/kittygram-final/blob/main/.github/workflows/main.yml)
## Описание проекта

Сайт с возможностью публикации фотографий котов и их достижений.

## Технологии

- Python 3.9
- Django 3.2.3
- Django REST framework 3.12.4
- JavaScript

## Запуск проекта из образов с Docker hub

Для локальногозапуска необходимо создать папку проекта, например `kittygram` и перейти в нее:

```bash
mkdir kittygram && cd kittygram
```

Затем создать .env файл. Пример env файла приведен ниже.
```bash
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost
```

В папку проекта копируем файл `docker-compose.production.yml` и запускаем его:

```bash
sudo docker compose -f docker-compose.production.yml up
```

Произойдет скачивание образов, создание и включение контейнеров, создание volume и сети.

## После запуска: Миграции, сбор статистики

После запуска необходимо выполнить сбор статистики и миграции бэкенда. Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается. 

```bash
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate

sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic

sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/static/
```

И далее проект доступен на: 

```
http://localhost:9000/
```

## Остановка сети контейнеров

В окне, где был запуск **Ctrl+С** или в другом окне:

```bash
sudo docker compose -f docker-compose.yml down
```


Норенко Евгений Викторович

E-mail: norugin@gmail.com
