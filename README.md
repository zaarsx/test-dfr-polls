Задание
=======

У текущего тестового задания есть только общее описание требований, конкретные детали реализации остаются на усмотрение разработчика.

##### 
Задача
 
Спроектировать и разработать API для системы опросов пользователей.

##### Функционал для администратора системы:

- авторизация в системе (регистрация не нужна)
- добавление/изменение/удаление опросов. Атрибуты опроса: название, дата старта, дата окончания, описание. После создания поле "дата старта" у опроса менять нельзя
- добавление/изменение/удаление вопросов в опросе. Атрибуты вопросов: текст вопроса, тип вопроса (ответ текстом, ответ с выбором одного варианта, ответ с выбором нескольких вариантов)

##### Функционал для пользователей системы:

- получение списка активных опросов
- прохождение опроса: в качестве идентификатора пользователя в API передаётся числовой ID, по которому сохраняются ответы пользователя на вопросы; один пользователь может участвовать в любом количестве опросов
- получение пройденных пользователем опросов с детализацией по ответам (что выбрано) по ID уникальному пользователя

##### Использовать следующие технологии
 
Django 2.2.10, Django REST framework.

##### Результат выполнения задачи:
- исходный код приложения в github (только на github, публичный репозиторий)
- инструкция по разворачиванию приложения (в docker или локально)
- документация по API


Документация 
============

## Установка

Установка проекта - стандартная. Настройте скачайте себе репозиторий

```
git clone https://github.com/zaarsx/test-dfr-polls.git
``` 

Создайте виртуальное оружение и установите пакеты из файла `requirements.txt`

```
pip install -r requirements.txt
```

Произведите настройку базы данных при необходимости.

Затем примените миграции и запустите проект.

```
python manage.py migrate
python manage.py runserver
```


## Справка по API

Доступ к методам API происходит по URL вида `<host>/api/v1/<method>/`.

### Список методов
* `poll`:
  * GET - предоставляет список активных опросов 
  * Возможна фильтрация по полям: `id`
* `question`:
  * GET - предоставляет список вопросов 
  * Возможна фильтрация по полям: `id`, `post`
* `answer`:
  * GET - предоставляет список вопросов 
  * Возможна фильтрация по полям: `id`, `question`
* `polling`:
  * POST - добавляет результат ответа на вопрос текущего пользователя в базу данных 
* `results`:
  * GET - возвращает список пройденых опросов, вопросы и список доступных ответов и предоставленных пользователем

### Администраторские методы

* `admin/poll`:
  * GET - список опросов
  * POST - новый опрос
  * PUT - изменение опроса. Обязателено параметр `id` в передаваемых данных
  * DELETE - удаление опроса. Обязателено параметр `id` в передаваемых данных


* `admin/question`:
  * GET - список вопросов
  * POST - новый вопрос
  * PUT - изменение вопроса. Обязателено параметр `id` в передаваемых данных
  * DELETE - удаление вопроса. Обязателено параметр `id` в передаваемых данных

* `auth/login` - Авторизация в системе

