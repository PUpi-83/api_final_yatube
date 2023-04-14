# API для Yatube :milky_way:
*Yatube - это проект социальной сети для публикации и обмена постами, фотографиями и комментариями. Проект реализован в виде веб-приложения с использованием Django и Django REST framework для создания REST API.*

## API проекта Yatube имеет следующие функции:
1. **Публикации:** API позволяет пользователям создавать, просматривать, обновлять и удалять посты. Посты могут содержать текст, изображения и относиться к определенной группе.

2. **Аутентификация и авторизация:** API позволяет пользователям регистрироваться, аутентифицироваться и авторизоваться с использованием JWT-токенов (Joser).

3. **Подписки:** API позволяет пользователям подписываться на других пользователей и просматривать список своих подписок.

4. **Группы:** Посты могут быть опубликованы в определенной группе, и пользователи могут просматривать список групп и постов в каждой группе.

5. **Пагинация:** API реализует пагинацию с использованием LimitOffsetPagination, что позволяет ограничивать количество возвращаемых объектов и указывать смещение для получения следующей порции данных.

6. **Авторизация и аутентификация:** API защищен авторизацией и аутентификацией, что означает, что некоторые эндпоинты доступны только авторизованным пользователям, а некоторые операции могут быть выполнены только автором объекта.

## Как запускаем проект:
##### Запускаем терминал. Клонируем репозиторий и переходим в него с помощью командной строки
```
git clone https://github.com/PUpi-83/api_final_yatube.git
```
##### После успешного клонирования переходим в сам проект
```
cd api_final_yatube
```
##### Следом создаём и активируем виртуальное окружение 
```
python -m venv venv
```
```
source venv/Scripts/activate
```
##### или
```
. venv/Scripts/activate
```
##### Обновляем pip, устанавливаем зависимости
```
python -m pip install --upgrade pip
```
```
python -m pip install -r requirements.txt
```
##### Выполняем миграции
```
python manage.py migrate
```
##### И запускаем проект
```
python manage.py runserver
```

## Примеры запросов
#### Для неавторизованных пользователей
```python
GET api/v1/posts/ - получение список всех публикаций
GET api/v1/posts/{id}/ - получение публикации по id.
GET api/v1/groups/ - получение списка доступных сообществ
GET api/v1/groups/{id}/ - получение информации о сообществе по id
GET api/v1/{post_id}/comments/ - получение всех комментариев к публикации
GET api/v1/{post_id}/comments/{id}/ - получение комментария к публикации по id
```

#### Для авторизованных пользователей
*Доступ авторизованным пользователям осуществляется с использованием JWT-токена (Joser), который можно получить, выполнив POST-запрос по адресу:*
```python
POST /api/v1/jwt/create/
```
*Придумываем логин и пароль, передаем в тело запроса:*
```python
{
"username": "string",
"password": "string"
}
```
*Для получения токена отправляем POST-запрос на эндпоинт ```/auth/jwt/create/```, передав в тело запроса логин и пароль, который использовался ранее
После получения добавляем токен в заколовок запроса в поле Authorization, перед самими токеном прописываем ключевое слово Bearer и пробел между ними.*

### И вуаля, теперь доступен весь функционал. Аплодисменты. 

##### Возвращаемся к примерам:
 Cоздание публикации
 ```python
 POST /api/v1/posts/
 ```
В теле запроса передаем:
```python
{
"text": "string",
"image": "string",
"group": 0
}
```
Обновление публикации.
```python
PUT /api/v1/posts/{id}/
```
В теле запроса передаем:
```python
{
"text": "string",
"image": "string",
"group": 0
}
```
Удаление публикации
```python
DELETE /api/v1/posts/{id}/
```
Получение списка подписок:
```python
GET /api/v1/follow/
```
В проекте API также реализована пагинация с использованием подхода LimitOffsetPagination. Вы можете использовать следующий синтаксис для получения постов с ограничением количества возвращаемых объектов и указанием смещения:
```python
GET /api/v1/posts/?limit=5&offset=0
```

### Автор :arrow_right: [Анастасия](https://github.com/PUpi-83)
