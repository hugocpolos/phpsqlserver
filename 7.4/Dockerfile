FROM ubuntu:20.04

ENV ACCEPT_EULA=Y 
ENV DEBIAN_FRONTEND=noninteractive
LABEL Author="Hugo Constantinopolos hugo.cpolos@gmail.com"
ENV PHP_VERSION=7.4

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php -y && \
    apt-get update && \
    apt-get install -y php${PHP_VERSION} php${PHP_VERSION}-dev php${PHP_VERSION}-xml -y --allow-unauthenticated && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    apt-get install -y msodbcsql17 && \
    apt-get install -y mssql-tools && \
    apt-get install -y unixodbc-dev && \
    pecl install sqlsrv && \
    pecl install pdo_sqlsrv && \
    printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/${PHP_VERSION}/mods-available/sqlsrv.ini && \
    printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/${PHP_VERSION}/mods-available/pdo_sqlsrv.ini && \
    phpenmod -v ${PHP_VERSION} sqlsrv pdo_sqlsrv && \
    apt-get install -y libapache2-mod-php${PHP_VERSION} apache2 && \
    a2dismod mpm_event && \
    a2dismod --force autoindex && \
    a2enmod mpm_prefork && \
    a2enmod php${PHP_VERSION} && \
    rm -r /var/www/html/* \
    apt-get remove -y software-properties-common gcc && \
    apt-get autoclean && \
    apt-get autoremove -y


EXPOSE 80
WORKDIR /var/www/html/
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
