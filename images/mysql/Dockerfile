FROM php:5.6-apache

RUN docker-php-ext-install mysqli pdo pdo_mysql
# RUN apt-get -y install mysqli pdo pdo_mysql pdo_pgsql
# RUN apt-get -y install mysqli
# RUN apt-get -y install mysqlnd
# RUN apt-get -y install mysql
# RUN apt-get -y install pdo
# RUN apt-get -y install pdo_mysql
# RUN apt-get -y install pdo_pgsql

CMD ["apache2-foreground"]