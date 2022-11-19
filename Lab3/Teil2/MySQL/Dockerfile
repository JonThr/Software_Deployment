FROM debian:jessie

RUN DEBIAN_FRONTEND=noninteractive
ENV container docker

ENV MYSQL_ROOT_PASSWORD=somewordpress
ENV MYSQL_DATABASE=wordpress
ENV MYSQL_USER=wordpress
ENV MYSQL_PASSWORD=wordpress

RUN apt update
RUN apt upgrade
RUN apt install -y wget
RUN apt install -y lsb-release
RUN wget http://repo.mysql.com/mysql-apt-config_0.8.9-1_all.deb
RUN dpkg -i mysql-apt-config_0.8.9-1_all.deb
RUN echo "mysql-server mysql-server/root_password password $MYSQL_ROOT_PASSWORD" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password $MYSQL_ROOT_PASSWORD" | debconf-set-selections
RUN apt install -y --force-yes mysql-server
RUN sed -i "s/.*bind-address.*/bind-address = 0.0.0.0/" /etc/mysql/my.cnf

VOLUME ["/var/lib/mysql/"]

EXPOSE 3306/tcp

CMD service mysql start && mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "CREATE USER '${MYSQL_USER}'@'%' IDENTIFIED BY '${MYSQL_PASSWORD}';" || true && \
mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "CREATE DATABASE IF NOT EXISTS ${MYSQL_DATABASE};" && \
mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "GRANT all privileges ON ${MYSQL_DATABASE}.* TO '${MYSQL_USER}'@'%';" \
mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "flush privileges;" && \
mysqld