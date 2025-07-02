[![Main Kittygram workflow](https://github.com/Konstantin-Kleinikov/kittygram_final/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/Konstantin-Kleinikov/kittygram_final/actions/workflows/main.yml)

#  Социальная сеть для домашних животных Kittygram

Адрес сайта: https://yp-pythoproject.sytes.net/

## Описание проекта

Данный проект представляет собой социальную сеть для домашних животных Kittygram, которая позволяет пользователям: 
- просматривать фотографии и достижения домашних животных
- регистрироваться и авторизовываться
- делиться фотографиями своих питомцев
- добавлять достижения своих питомцев

## Использованные технологии
- Python — разработка backend
- Django — веб-фреймворк
- Django REST Framework — создание API
- JavaScript — разработка frontend
- React — фреймворк для frontend
- Nginx — веб-сервер и обратный прокси
- Docker — контейнеризация и деплой
- PostgreSQL — база данных
- GitHub Actions — автоматизация CI/CD
- pytest — тестирование backend
- npm — управление пакетами frontend


## Как развернуть проект локально

### 1. Клонируйте репозиторий на компьютер

### 2. Заполните переменные окружения
Для корректной работы проекта необходимо заполнить переменные окружения. Создайте файл `.env` в 
корневой директории проекта и добавьте в него следующие переменные:

```env
- SECRET_KEY=your_django_secret_key
- DEBUG=True
- ALLOWED_HOSTS=your_domain.com,localhost,127.0.0.1
- DB_ENGINE=sqlite
- DB_NAME=your_db_name
- POSTGRES_USER=your_db_user
- POSTGRES_PASSWORD=your_db_password
- DB_HOST=db
- DB_PORT=5432
```
### 3. Установите зависимости и выполните миграции
В терминале перейдите в директорию backend и выполните следующие команды:

```python
pip install -r requirements.txt
python manage.py migrate
```
### 4. Запустите frontend-проект
```bash
npm run start
```
### 5. Запустите backend-проект
```bash
python manage.py runserver
```
### 6. Откройте в браузере адрес http://localhost:3000


## Как развернуть проект на удаленном сервере

### 1. Создайте каталог проекта
Зайдите на удаленный сервер и в директории /home/<user>/ создайте каталог kittygram.

### 2. Заполните переменные окружения
Для корректной работы проекта необходимо заполнить переменные окружения. Создайте файл `.env` в 
корневой директории проекта kittygram и добавьте в него следующие переменные:

```env
- SECRET_KEY=your_django_secret_key
- DEBUG=False
- ALLOWED_HOSTS=your_domain.com,localhost,127.0.0.1
- DB_ENGINE=postgres
- DB_NAME=your_db_name
- POSTGRES_USER=your_db_user
- POSTGRES_PASSWORD=your_db_password
- DB_HOST=db
- DB_PORT=5432
```
### 3. Заполните переменные Secrets в GitHub
В Settings проекта перейдите в Secrets and variables и зайдите на страницу Actions.
Заполните следующие Repository secrets:
```env
- DOCKER_USERNAME=your_docker_hub_username
- DOCKER_PASSWORD=your_docker_hub_password
- HOST=remote_server_host_ip
- USER=your_remote_server_user
- SSH_KEY=your_ssh_private_key
- SSH_PASSPHRASE=your_ssh_pass_phrase
- TELEGRAM_TO=your_telegram_chat_id
- TELEGRAM_TOKEN=your_telegram_token_to_access_api
```

### 4. Выполните push из локального сервера, чтобы запустился GitHub Action

### 5. Дождитесь сообщения от Telegram Bot

## Как проверить работу с помощью автотестов

В корне репозитория создайте файл tests.yml со следующим содержимым:
```yaml
repo_owner: ваш_логин_на_гитхабе
kittygram_domain: полная ссылка (https://доменное_имя) на ваш проект Kittygram
taski_domain: полная ссылка (https://доменное_имя) на ваш проект Taski
dockerhub_username: ваш_логин_на_докерхабе
```

Скопируйте содержимое файла `.github/workflows/main.yml` в файл `kittygram_workflow.yml` в корневой директории проекта.

Для локального запуска тестов создайте виртуальное окружение, установите в него зависимости из backend/requirements.txt и запустите в корневой директории проекта `pytest`.

## Автор проекта
[Константин Клейников](https://github.com/Konstantin-Kleinikov) в рамках обучения
на Яндекс.Практикум по программе Python-разработчик расширенный (когорта 57+).
