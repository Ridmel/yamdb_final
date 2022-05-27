API (Django REST framework) площадки для размещения рецензий и отзывов на фильмы, музыку и литературу с готовой инфраструктурой (Nginx, Gunicorn, PostgreSQL), с настроенным CI/CD workflow (GitHub actions), с размещением в Docker контейнерах.  



### *Запуск в контейнере*

Клонировать репозиторий:

    git clone git@github.com:Ridmel/yamdb_final.git


*(Инструкция по установке docker и docker-compose доступна на официальном [сайте](https://docs.docker.com/engine/install/))*
\
\
В директории `yamdb_final/infra/` создать *.env* файл. Пример заполнения:

    SECRET_KEY=secret
    POSTGRES_DB=postgres
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=password
    DB_ENGINE=django.db.backends.postgresql
    DB_HOST=db
    DB_PORT=5432
\
Из директории `yamdb_final/infra/` выполнить команды:

    docker-compose up -d
    docker-compose exec web python manage.py migrate
    docker-compose exec web python manage.py createsuperuser
    docker-compose exec web python manage.py collectstatic --no-input 
\
 Чтобы заполнить базу данных тестовыми записями (фикстурами), выполнить из `../yamdb_final/infra/`:
 

    docker exec -i ridmel_web_1 python manage.py loaddata --format=json - < fixtures.json
\
Теперь сайт доступен через браузер в том числе и по локальному адресу `http//:127.0.0.1/`\
Документация API (redoc) `http//:127.0.0.1/redoc/`\
Админский кабинет `http//:127.0.0.1/admin/`
\
\
\
*Автор: Роман Сергиенко* 
