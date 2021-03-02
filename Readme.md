# Docker config

Add a symfony project
> symfony new --full demo

Copy that file at the root of the project
````
FROM php:7.3.27-fpm-alpine
RUN apk --update --no-cache add git
RUN docker-php-ext-install pdo_mysql pcntl
COPY --from=composer /usr/bin/composer /usr/bin/composer
WORKDIR /var/www
CMD composer install; php-fpm
EXPOSE 9000
````

To start the application
> docker-compose up -d

To stop the application
> docker-compose stop

To list the containers
> docker-compose ps

````
Warning :
You might expect some 502 Bad Gateway errors from nginx
while the container php_fpm is downloading all the symfony
requirements ...
`````
You can monitor that for now with :
> docker-compose logs php

and wait for
````
php_fpm       | [02-Mar-2021 13:00:19] NOTICE: fpm is running, pid 1
php_fpm       | [02-Mar-2021 13:00:19] NOTICE: ready to handle connections
````
to be shown :)

App is served in localhost:8020 on the host, you can change this by changing the docker-compose.yml file
