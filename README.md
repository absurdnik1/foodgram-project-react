# praktikum_new_diplom
server_name = foodgramforeveryone.ddns.net
admin_login = jesyur21@gmail.com
admin_password = 161718admin

Инструкция для разворачивания проекта на удаленном сервере:
Склонируйте проект из репозитория:
$ git clone https://github.com/absurdnik1/foodgram-project-react.git
Выполните вход на удаленный сервер

Установите DOCKER на сервер:

apt install docker.io 
Отредактируйте конфигурацию сервера NGINX:
Локально измените файл ..infra/nginx.conf - замените данные в строке server_name на IP-адрес удаленного сервера
Скопируйте файлы docker-compose.yml и nginx.conf из директории ../infra/ на удаленный сервер

Установите и активируйте виртуальное окружение (для Windows):

python -m venv venv 
source venv/Scripts/activate
python -m pip install --upgrade pip
Запустите приложение в контейнерах:
docker-compose up -d --build
Выполните миграции:
docker-compose exec backend python manage.py migrate
Создайте суперпользователя:
docker-compose exec backend python manage.py createsuperuser
Выполните команду для сбора статики:
docker-compose exec backend python manage.py collectstatic 
Команда для заполнения тестовыми данными:
docker-compose exec backend python manage.py load_ingredients
Команда для остановки приложения в контейнерах:
docker-compose down -v
Для запуска на локальной машине:
Склонируйте проект из репозитория:
$ git clone https://github.com/absurdnik1/foodgram-project-react.git
В папке ../infra/ заполните .env своими данными:
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
SECRET_KEY=<...> # секретный ключ django-проекта из settings.py
Создайте и запустите контейнеры Docker (по инструкции выше).
После запуска проект будут доступен по адресу: http://localhost/

Документация будет доступна по адресу: http://localhost/api/docs/

Особенности заполнения данными:
Добавьте теги для для рецептов через админ-панель проекта http://localhost/admin/, т.к. это поле является обязательным для сохранения рецепта и добавляется только админом.
