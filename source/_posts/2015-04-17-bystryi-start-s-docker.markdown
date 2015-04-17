---
layout: post
title: "Быстрый старт с Docker"
date: 2015-04-17 13:23:43 +0300
comments: true
categories: Разработка
---
Давно собирался - и вот пришел момент необходимости начать использовать _Docker_, вместо привычного _Vagrant_. Все не хватало времени разобраться с ним и особо пугали длинные строчки для запуска контейнера, вместо привычного `vagrant up`.
Как оказалось, в _Docker_ тоже есть легкий старт - `docker compose`.<!--more-->

Подробно почитать о установке и использовании можно [в оригинале](https://docs.docker.com/compose/). 

Установка *compose* производится отдельно от _Docker_:
```
curl -L https://github.com/docker/compose/releases/download/1.2.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
Также можно использовать _Python package_
```
sudo pip install -U docker-compose
```
После этого привычный запуск сервера превращается в команду `docker-compose up`. 

###Конфигурация для запуска PHP проекта
Достаточно добавить к проекту пару файлов

_Dockerfile:_
```
# построить на базе официального контейнера
FROM php:5.6-apache 
# включить rewrite модуль апаче
RUN a2enmod rewrite 
# установка дополнительных php модулей
RUN docker-php-ext-install mysql mysqli pdo pdo_mysql 

```
_docker-compose.yaml:_
```
web:
  # Используем Dockerfile из текущей директории для построения образа
  build: .
  # Соединить с контейнером db
  links:
   - db:mysql
  # Открыть порт контейнера
  ports:
   - 8080:80
  # использовать исходники из текущей директории 
  volumes: 
   - .:/var/www/html

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: example
    MYSQL_USER: wp_user
    MYSQL_PASSWORD: password
    MYSQL_DATABASE: wordpress
  volumes:
  # хранить данные бд в отдельном контейнере
    - /var/lib/mysql

```
`docker-compose up`