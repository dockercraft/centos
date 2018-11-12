# How-To
 # Local Build: docker build -t php .
 # Local Run: docker run -it --rm php

FROM centos:7.5.1804
MAINTAINER Duan Li <inputx@goodays.com>

# User/Group
ENV MY_USER="www-data" \
	MY_GROUP="www-data" \
	MY_UID="1000" \
	MY_GID="1000"

RUN groupadd -g ${MY_GID} -r ${MY_GROUP} && \
	adduser -u ${MY_UID} -m -s /bin/bash -g ${MY_GROUP} ${MY_USER} && \
	yum update -y && \
	yum install unzip git yum-utils php php-cli php-fpm php-common php-bcmath php-ldap php-mcrypt php-mbstring php-gd php-opcache php-odbc php-soap php-xml php-xmlrpc php-mysql php-pgsql php-pdo -y && \
	php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php -r "if (hash_file('sha384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
	php composer-setup.php --install-dir=bin --filename=composer && \
	php -r "unlink('composer-setup.php');" && \
	yum clean all && \
	rm -rf /var/cache/yum && \
	composer global require "hirak/prestissimo" -v && \
	composer global require "phpunit/phpunit" "codeception/codeception" -v && \
	composer clearcache
	

ENV PATH="/root/.composer/vendor/bin:${PATH}"

EXPOSE 80 8000 8080 8008 8800 9000 443

