ARG VERSION=8.2

FROM "php:${VERSION}-alpine"

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/conf.d/php.ini"

RUN apk add git

RUN git config --global --add safe.directory /var/source

RUN php -r \
    "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r \
    "if (hash_file('sha384', 'composer-setup.php') === 'c8b085408188070d5f52bcfe4ecfbee5f727afa458b2573b8eaaf77b3419b0bf2768dc67c86944da1544f06fa544fd47') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }"
RUN php composer-setup.php \
    --install-dir=/usr/local/bin \
    --filename=composer
RUN php -r "unlink('composer-setup.php');"
