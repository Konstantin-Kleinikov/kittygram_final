# Ревью 1

## settings.py

```python
SECRET_KEY = os.getenv('SECRET_KEY', 'default-key')
```
Можно указать дефолтное значение с помощью `get_random_secret_key` из `django.core.management.utils`

```python
DEBUG = True
```

Рекомендуется хранить параметр `DEBUG` в переменной окружения, это даст возможность включать/выключать отладочный режим приложения в зависимости от текущего окружения. Из `env` возвращаются строки, переменной DEBUG требует булевое значение. В таком случае сработает приведение типов и будь то `'True'` или `'False'`, а любая непустая строка будет приведена к `True`. Потому что `bool('') = False`, а любая непустая строка будет приведена к `True`. Лучше сравнивать строку, возвращаемую из `env` с `'true'`, используя метод `.lower`, чтобы не учитывать регистр символов.

```python
ALLOWED_HOSTS = ['84.201.137.0', '127.0.0.1', 'yp-pythoproject.sytes.net', 'localhost']
```
Хранение `ALLOWED_HOSTS` в переменных среды (`env`) является хорошей практикой с точки зрения безопасности и позволит избежать возможных утечек информации. Так как `ALLOWED_HOSTS` это список, а из `env` приходят строки, не забудь применить метод `.split`. Для дефолта можно задать дефолтное значение в виде `localhost` и `127.0.0.1` через разделитель указанный в сплите.

```python
DATABASES = {}
```
Если нужно что-то быстро протестировать удобно работать с `sqlite`, поэтому можно предусмотреть условие, если специальная переменная из `env` есть, то база `sqlite`, иначе - `postgresql`.

```python
}
```
В конце документа нужно оставлять пустую строку.  
[https://stackoverflow.com/questions/2287967/why-is-it-recommended-to-have-empty-line-in-the-end-of-a-source-file](https://stackoverflow.com/questions/2287967/why-is-it-recommended-to-have-empty-line-in-the-end-of-a-source-file).

## backend / README.md

ReadMe можно удалить, есть в корне проекта.

## nginx.conf

```python
server {
	listen 80;
	index index.html;
```
Лучше скрыть от пользователей версию `nginx`. Им это ни к чему, а потенциальному недоброжелателю может быть полезно. [Документация](https://nginx.org/ru/docs/http/ngx_http_core_module.html#server_tokens).

## README.md

Нужен бейджик об удачно завершенном workflow и предоставить доступ к гиту, чтобы его посмотреть(ник Port-tf). [Документация](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge).

Файл README - это "лицо" проекта. В нем хорошо бы расписать:

- полное описание, что это за проект, для чего, какие функции выполняет.
- стек использованных технологий.
- как развернуть проект
- как заполнить `env`
- кто автор

README оформляется на языке [Markdown](https://texterra.ru/blog/ischerpyvayushchaya-shpargalka-po-sintaksisu-razmetki-markdown-na-zametku-avtoram-veb-razrabotchikam.html).

## docker-compose.production.yml

```yaml
depends_on:
```
Контейнер `gateway` не должен подниматься, пока не поднимется бэк и **фронт**. Нужно прописать [зависимость](https://docs.docker.com/reference/compose-file/services/#depends_on).

## docker-compose.yml

Лишний файл в гите, нужен только при запуске локально.

## kittygram_workflow.yml

```yaml
name: Main Kittygram workflow
```
Тесты должны запускаться при пуше в любую ветку. А вот сборки и деплой - только в основную ветку. Как это сделать можно посмотреть [тут](https://stackoverflow.com/a/73624365).

```yaml
# Блок services аналогичен docker-compose.yml
```
Обилие комментариев перегружает сам код и он становится менее читаемый.

```yaml
python-version: 3.9
```
Можно проверять на нескольких версиях параллельно. Например, `3.8`, `3.9`, `3.10`, см. `matrix` в [документации](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python).

```yaml
build_and_push_to_docker_hub:
```
Чтобы повысить читаемость, лучше отделять ворки пустой строкой.

```yaml
tags: kkleinikov/kittygram_backend:latest
```
Лучше ник убрать в секреты. В остальных билдах ниже тоже.


```yaml
message: Деплой успешно выполнен!
```
Сообщение отсылаемое в телегу может быть полезней, например можно указать, кто сделал push `(github.actor)` и сообщение коммита `(github.event.commits[0].message)`. Можно также дать ссылку на коммит: `https://github.com/${{ github.repository }}/commit/${{github.sha}}`. [Документация](https://docs.github.com/en/actions/learn-github-actions/contexts#github-context).
