FROM debian:10

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get install -y php-fpm && \
    apt-get install -y php-mysql && \
    apt-get install -y mariadb-client && \
    curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp && \
    apt-get remove -y curl && \
    apt-get clean

ARG VOLUME

RUN mkdir -p /run/php ${VOLUME}

EXPOSE 9000

COPY /config/wp /etc/php/7.3/fpm/pool.d/www.conf

WORKDIR ${VOLUME}

COPY /config/entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
