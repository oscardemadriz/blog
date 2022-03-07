---
layout: post
read_time: true
show_date: true
title: "Docker + Wordpress"
img: uploads/whale.jpg
date: 2021-09-20
tags: [docker, tips]
category: tutorials
author: Oscar Sanchez
---
En uno de los proyectos en los que estamos trabajando para un cliente, hemos tenido que levantar un wordpress con varias extensiones, para ello partimos de la base de wordpress y añadimos las extensiones necesarias en el `Dockerfile` para generar la imagen lista:
```yaml
FROM wordpress:4.9 as my-wordpress


RUN  docker-php-ext-install mbstring && docker-php-ext-install exif
```

El comando `docker-php-ext` añadirá las extensiones directamente al Apache.

El siguiente paso sería generar un `docker-compose.yml` con la DB:
```yaml
version: "3.3"
services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: "db"
      MYSQL_USER: "user"
      MYSQL_PASSWORD: "nutty_yippee"
      MYSQL_ROOT_PASSWORD: nutty_yippee
    ports:
      - "3306:3306"
    expose:
      - "3306"
    volumes:
      - db:/var/lib/mysql
  wordpress:
    build: .
    environment:
      WORDPRESS_DB_NAME: "db"
      WORDPRESS_DB_USER: "user"
      WORDPRESS_DB_HOST: "db"
      WORDPRESS_DB_PASSWORD: "nutty_yippee"

    ports:
      - "80:80"
    expose:
      - "80"
    volumes:
      - ./public:/var/www/html
    mem_limit: 1g

# Names our volume
volumes:
  db:

``` 

Dentro de la carpeta `public` es donde ubicaremos los archivos del Wordpress (wp-content / wp-admin).

Finalmente para lanzar el docker `docker compose up`.

## LEVEL UP
Si añadimos un alias en windows creando un archivo `%userprofile%/dcu.cmd` con el comando:
```
@echo off
docker compose up
```
Podemos levantar los contenedores con tan solo `dcu` en la terminal:
```cmd
PS C:\Users\CDistrict\Documents\blog\tmp> dcu
[+] Running 2/2
 - Container tmp_db_1         Created                                                                                                                                                                                                       0.0s 
 - Container tmp_wordpress_1  Recreated                                                                                                                                                                                                     1.1s 
Attaching to db_1, wordpress_1
```
Photo by <a href="https://unsplash.com/@mikedoherty?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Mike Doherty</a> on <a href="https://unsplash.com/s/photos/whale?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  