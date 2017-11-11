# docker-dev


## Get the files
```
sudo git clone https://github.com/miguelcarrascoq/docker-dev.git
cd docker-dev
```

## Build Apache-PHP-Oracle & run
```
cd images/apache-php-oracle/
docker build -t miguelcarrascoq/docker-dev .

docker-compose up
```

## Build MySQL
```
cd images/mysql
docker build -t miguelcarrascoq/php-mysql .

docker run --name php-mysql -v "$PWD/":/var/www/html miguelcarrascoq/php-mysql
```

## Enter to bash
```
docker exec -it dev-env bash
```