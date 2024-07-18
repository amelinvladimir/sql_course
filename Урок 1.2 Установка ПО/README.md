# Установка ПО

## Этап 1. Установка DBeaver - клиента для работы к СУБД.

#### Шаг 1. Скачиваем дистрибутив для своей операционной системы по ссылке [ссылке](https://dbeaver.io/download/).
#### Шаг 2. Устанавливаем DBeaver из дистрибутива.
#### Шаг 3. Запускаем DBeaver, проверяем, что он запущен.
![image](https://github.com/user-attachments/assets/77e22364-56cd-4ca2-bce5-00c0a8872031)

## Этап 2. Установка PostgreSQL.

### Вариант установки 1. Локально из дистрибутива.

#### Шаг 1. Скачиваем дистрибутив PostgreSQL с [сайта](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).
Выбираем дистрибутив c последней доступной версии на вашей операционной системе (ОС).
После нажатия на ссылку откроется окно, в котором скачивание должно начаться автоматически.

Если скачивание не начнется автоматически, то нажмите по ссылке:

![image](https://github.com/amelinvladimir/sql_course/assets/8919281/59580112-75b4-40b0-a86e-a0378fc48845)

#### Шаг 2. Устанавливаем PostgreSQL из дистрибутива.
Запустите установку из дистрибутива.

При выборе списка компонентов для установки нужно снять галочку с pgAdmin
![image](https://github.com/amelinvladimir/sql_course/assets/8919281/09cdaeea-b35e-4dd1-8f21-cb69cd8925e6)

В остальных пунктах оставьте значения по умолчанию и начните установку.

После завершения установки снимите галочку со Stack Builder и завершите установку:
![image](https://github.com/user-attachments/assets/2752e447-9632-42f3-a26f-05bb26aa50c9)


### Вариант установки 2. Из docker образа.

#### Шаг 1. Устанавливаем Docker Desktop, если если он еще не установлен на компьютере.
[Инструкция по установке Docker Desktop и wsl2 на Windows 10.](https://github.com/amelinvladimir/docker_course/blob/main/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20Docker%20%D0%BD%D0%B0%20Windows%2010/README.md)

Для установки на MacOS скачайте дистрибутив по [ссылке](https://www.docker.com/products/docker-desktop/) и затем установите его.


#### Шаг 2. Запускаем приложение Docker Desktop.

#### Шаг 3. Открываем командную строку.
На MacOS открываем обычный терминал.
![image](https://github.com/user-attachments/assets/12d6d947-aa2a-4ed0-aa83-864026e38b76)

В Windows открываем приложение "Терминал", нажимаем на стрелку вниз в списке вкладок и выбираем "Ubuntu ...".

#### Шаг 4. Запускаем контейнер с PostgreSQL.

Для запуска контейнера с postgres версии 16.3, на которой проверена данная инструкция, выполните команду:

````
docker run --name postgresdb -e POSTGRES_PASSWORD=pass -d -p 5432:5432 postgres:16.3
````

Параметры для подключения к postgres:
```
Хост: localhost
Порт: 5432
База данных: postgres
Пользователь: postgres
Пароль: pass
```

если вы получите ошибку "bind: address already in use", то измените "-p 5432:5432" на "-p 5434:5432". В этом случае порт для подключения к postgres будет 5434.

Для запуска контейнера с последней версии postgres выполните команду:

````
docker run --name postgresdb -e POSTGRES_PASSWORD=pass -d -p 5432:5432 postgres
````


## Этап 3. Подключаемся к базе данных с помощью DBeaver.

#### Шаг 1. Открываем DBeaver.

#### Шаг 2. Создаем новое подключение.
Жмем на стрелку вниз рядом с розеткой с плюсиком и выбираем Postgres. 
![image](https://github.com/user-attachments/assets/6cc52a7a-2dfc-4b69-9ad3-c75f724c7bc0)

Скачиваем файлы драйвера, если будет открыто соответствующее окно:
![image](https://github.com/user-attachments/assets/b88b49dc-e6b3-44a3-a460-151cc524185a)

#### Шаг 3. Указываем параметры подключения и проверяем подключение.

```
Хост: localhost
Порт: 5432
База данных: postgres
Пользователь: postgres
```
Если вы установили postgres из дистрибутива, то нужно указать пароль, который вы задали при установке.
Если вы развернули postgres в контейнере, то используйте пароль pass

Нажмите "Тест соединения".
Если вы увидите "Соединено", значит подключение настроено корректно.
![image](https://github.com/user-attachments/assets/c69eca8c-535f-45bf-9ac8-bbfb68e8c710)

Нажмите "Ок".

## Этап 4. Разворачиваем учебную базу данных.

#### Шаг 1. Скачиваем учебную бд.
[Ссылка для скачивания](https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/).


## Этап 5. Устанавливаем инструмент, который умеет делать скриншоты.
