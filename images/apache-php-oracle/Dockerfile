FROM debian:jessie

RUN apt-get update && apt-get -y upgrade

# Install Apache2 / PHP 5.6 & Co.
RUN apt-get -y install apache2      
RUN apt-get -y install php5
RUN apt-get -y install libapache2-mod-php5
RUN apt-get -y install php-pear
RUN apt-get -y install libaio1
RUN apt-get -y install vim
RUN apt-get -y install php5-common
RUN apt-get -y install php5-cli
RUN apt-get -y install php5-gd
RUN apt-get -y install php5-json
RUN apt-get -y install php5-ldap
RUN apt-get -y install php5-mysql
RUN apt-get -y install php5-pgsql
RUN apt-get -y install php5-cgi
RUN apt-get -y install php5-dev
# RUN apt-get -y install php5-pdo (no funciona)

# Install the Oracle Instant Client
ADD to-copy/oracle/oracle-instantclient12.1-basic_12.1.0.2.0-2_amd64.deb /tmp
ADD to-copy/oracle/oracle-instantclient12.1-devel_12.1.0.2.0-2_amd64.deb /tmp
ADD to-copy/oracle/oracle-instantclient12.1-sqlplus_12.1.0.2.0-2_amd64.deb /tmp
RUN dpkg -i /tmp/oracle-instantclient12.1-basic_12.1.0.2.0-2_amd64.deb
RUN dpkg -i /tmp/oracle-instantclient12.1-devel_12.1.0.2.0-2_amd64.deb
RUN dpkg -i /tmp/oracle-instantclient12.1-sqlplus_12.1.0.2.0-2_amd64.deb
RUN rm -rf /tmp/oracle-instantclient12.1-*.deb

# Enable apache mods.
RUN a2enmod php5
RUN a2enmod rewrite

# Copy HTTP server config
RUN chmod 755 /etc/apache2/sites-available/
RUN rm -f /etc/apache2/sites-available/000-default.conf
ADD to-copy/000-default.conf /etc/apache2/sites-available/
#RUN ln -s /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-enabled/000-default.conf

RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

RUN mkdir /var/www/html/web
RUN mkdir /var/www/html/web/app
RUN mkdir $HOME/www
RUN mkdir $HOME/db_data
# COPY to-copy/sample/* /var/www/html/web
COPY to-copy/sample/* $PWD

# Set up the Oracle environment variables
ENV LD_LIBRARY_PATH /usr/lib/oracle/12.1/client64/lib/
ENV ORACLE_HOME /usr/lib/oracle/12.1/client64/lib/

# Install the OCI8 PHP extension
RUN echo 'instantclient,/usr/lib/oracle/12.1/client64/lib' | pecl install -f oci8-2.0.8
RUN echo "extension=oci8.so" > /etc/php5/apache2/conf.d/30-oci8.ini

# Set up the Apache2 environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80 3306

# Run Apache2 in Foreground
CMD /usr/sbin/apache2 -D FOREGROUND
