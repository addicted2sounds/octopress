---
layout: post
title: "Добавляем SkyDNS к среде разработки на Docker"
date: 2015-04-21 20:10:02 +0300
comments: true
categories: ['Docker', 'Разработка'] 
---
[SkyDns](https://github.com/skynetservices/skydns1) - это маленький динамический DNS сервер, написаный на `Go`. Для автоматического назначения доменов контейнерам докера можно использовать [SkyDock](https://github.com/crosbymichael/skydock). Такая связка позволяет не мучиться с поиском айпи нужного контейнера в системе или запускать несколько контейнеров и позволить им общаться между собой. Кому лень читать горы документации или лень учить английский, читаем дальше.
<!--more-->

Для начала нужно получить образы вышеназванных утилит.
```
docker pull crosbymichael/skydns
docker pull crosbymichael/skydock

```
После закачки образов можно приступить к созданию контейнеров: 
``` 
docker run -d -p 172.17.42.1:53:53/udp --name skydns crosbymichael/skydns -nameserver 8.8.8.8:53 -domain dev 

```
``` 
docker run -d -v /var/run/docker.sock:/docker.sock --name skydock crosbymichael/skydock -ttl 30 -environment dev -s /docker.sock -domain docker -name dev 
```

Вместо ```-domain dev ``` и ``` -name dev ``` выбираем любую понравивушюся доменную зону. ``` -nameserver 8.8.8.8:53 ``` указывает каким нс сервером пользоваться, если спрашивается неизвестный SkyDns адрес. 

Теперь можно легко стартовать
``` 
docker start skydock
docker start skynds 

```
или останавливать связку 

``` 
docker stop skydock
docker stop skynds 

```
Для удобства можно добавить старт сервисов в автозагрузку. 

Для Ubuntu, делается так:
```
sudo nano /etc/systemd/system/skydns.service

```
```
[Unit]
Description=SkyDNS
Requires=docker.service

[Service]
Restart=always
ExecStart=/usr/bin/docker start -a skydns
ExecStop=/usr/bin/docker stop -t 2 skydns

[Install]
WantedBy=multi-user.target

```
```
sudo nano /etc/systemd/system/skydock.service

```
```
[Unit]
Description=SkyDock
After=docker.service
Requires=skydns.service

[Service]
Restart=always
ExecStart=/usr/bin/docker start -a skydock
ExecStop=/usr/bin/docker stop -t 2 skydock

[Install]
WantedBy=multi-user.target

```
Теперь осталось прописать хост для контейнера. Для примера с compose, это делается просто (на примере к нашей [среде разработки](/bystryi-start-s-docker.html) для php):

```
web:
  build: .
  hostname: project.dev
  links:
   - db:mysql
  expose:
  - 80
  volumes: 
   - ./web:/var/www/html

db:
  image: mariadb
  hostname: db.project.dev
  environment:
    MYSQL_ROOT_PASSWORD: password
    MYSQL_USER: user
    MYSQL_PASSWORD: password
    MYSQL_DATABASE: project
  volumes:
    - /var/lib/mysql

```
