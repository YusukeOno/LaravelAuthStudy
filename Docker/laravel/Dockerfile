FROM centos:centos8
LABEL Name=laravelauthstudy Version=0.0.1

ENV LC_ALL=C

RUN dnf -y update && \
    dnf -y install glibc-langpack-ja httpd php php-pdo php-mysqlnd php-json php-mbstring php-xml zip npm && \
    dnf clean all

WORKDIR /var/www/local.laravel-auth

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    php -r "unlink('composer-setup.php');" && \
    composer global require hirak/prestissimo && \
    composer create-project --prefer-dist laravel/laravel . "6.*" && \
    chmod -R 777 /var/www/local.laravel-auth/storage && \
    npm install && \
    npm run dev

COPY ./Docker/laravel/my-vhost.conf /etc/httpd/conf.d
COPY ./Docker/laravel/00-mpm.conf /etc/httpd/conf.modules.d

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
