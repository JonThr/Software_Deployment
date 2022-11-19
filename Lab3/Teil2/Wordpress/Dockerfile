FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
ENV container docker

RUN apt update
RUN apt upgrade

RUN apt install -y wget
RUN apt install -y apache2
RUN apt install -y php5 libapache2-mod-php5 php5-mcrypt php5-mysql

RUN apt install unzip -y

RUN cd /var/www/html && \
    wget https://wordpress.org/latest.zip && \
    unzip -q latest.zip && \
    chown -R www-data:www-data /var/www/html/wordpress && \
    chmod -R 755 /var/www/html/wordpress && \
    mkdir -p /var/www/html/wordpress/wp-content/uploads && \
    chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads && \
    rm latest.zip

EXPOSE 80
VOLUME ["/var/www/html"]
CMD apachectl -D FOREGROUND