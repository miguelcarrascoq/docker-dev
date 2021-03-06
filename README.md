# docker-dev

Create a developer environment. The stack include:
- SO Debian 4.9.51 (jessie)
- Apache 2.0
- PHP 5.6.30
- Oracle with OCI8 Support & Run-time client v12.1.0.2.0
- MySQL & MySQL driver for PDO

## Steps
- Install Docker & Docker Compose
- Get the files
- Build the images
- Run the server

___

### Install Docker & Docker Compose
Go to https://www.docker.com/get-docker and get the Docker CE (Comumnity Edition)

### Get the files
```
sudo git clone https://github.com/miguelcarrascoq/docker-dev.git
cd docker-dev
```

### Build Apache-PHP-Oracle & run
```
cd images/apache-php-oracle/
docker build -t miguelcarrascoq/docker-dev .

sudo docker-compose up -d
```

### Build MySQL
```
cd images/mysql
docker build -t miguelcarrascoq/php-mysql .

docker run --name php-mysql -v "$PWD/":/var/www/html miguelcarrascoq/php-mysql
```

And then, you can use some MySQL DB client like "Sequel Pro" to manage the DB using this data:
- host: 127.0.0.1
- user: root
- pass: example

### Enter to bash
```
docker exec -it dev-env bash
```

### Run the server
Go to http://localhost

### Other commands
```
docker ps
docker stop dev-env
```

### OSX Hosts config. In /etc/hosts add
```
127.0.0.1       localhost
127.0.0.1       sbyc.byc.local
```

