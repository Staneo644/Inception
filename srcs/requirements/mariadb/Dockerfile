FROM debian:10

RUN apt-get update && \
    apt install -y mariadb-server && \
    apt-get clean

EXPOSE 3306

ARG MYSQL_ROOT_PASSWORD
ARG MYSQL_DATABASE
ARG MYSQL_USER
ARG MYSQL_PASSWORD

RUN service mysql start\
    && mysql -u root -e "CREATE DATABASE IF NOT EXISTS ${MYSQL_DATABASE};"\
    && mysql -u root -e "CREATE USER '${MYSQL_USER}'@'%' IDENTIFIED BY '${MYSQL_PASSWORD}';"\
    && mysql -u root -e "GRANT ALL PRIVILEGES ON ${MYSQL_DATABASE}.* TO ${MYSQL_USER}@'%';"\
    && mysql -u root -e "FLUSH PRIVILEGES;" \
    && mysql -u root -e "ALTER USER 'root'@'localhost' IDENTIFIED BY '${MYSQL_ROOT_PASSWORD}';"

#ENTRYPOINT ["mysqld"]
CMD [ "mysqld", "--bind-address=0.0.0.0", "--port=3306"]