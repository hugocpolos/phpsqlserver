# Docker image with PHP + APACHE + SQLSERVER DRIVERS

All images were built accordingly to the tutorial available at [Linux and macOS Installation Tutorial for the Microsoft Drivers for PHP for SQL Server](https://docs.microsoft.com/en-us/sql/connect/php/installation-tutorial-linux-mac).

## How to use it

### Building an image
```bash
# for php7.3
docker build -t php-sqlserver:7.3 ./7.3

# for php7.4
docker build -t php-sqlserver:7.4 ./7.4

# for php8.0
docker build -t php-sqlserver:8.0 ./8.0
```

### Running a built image
```bash
# for php7.3, using the port 8080
docker run -p 8080 php-sqlserver:7.3

# for php7.4, using the port 8080
docker build -t php-sqlserver:7.4 ./7.4

# for php8.0, using the port 8080
docker build -t php-sqlserver:8.0 ./8.0
```

### Using these images in a Dockerfile
```dockerfile
FROM php-sqlserver:7.3

RUN echo "<?php phpinfo(); ?>" > /var/www/html/index.php

# or

ADD <dir_with_php_files> /var/www/html
```