# Zend Server
#
# Version 0.2

# TODO:

FROM ubuntu:14.04

RUN apt-key adv --keyserver pgp.mit.edu --recv-key 799058698E65316A2E7A4FF42EAE1437F7D2C623
RUN echo "deb http://repos.zend.com/zend-server/8.0/deb_apache2.4 server non-free" >> /etc/apt/sources.list.d/zend-server.list
RUN apt-get update && apt-get install -y git zend-server-php-5.5 php5-mssql && /usr/local/zend/bin/zendctl.sh stop

COPY ./scripts /usr/local/bin
COPY ./libmysqlclient.so.18 /usr/lib/x86_64-linux-gnu/
COPY ./Zray /usr/local/zend/var/zray/extensions/

RUN rm /var/www/html/index.html
COPY ./app /var/www/html

# Make Apache run as the 'zend' user
RUN sed -i 's/www-data/zend/g' /etc/apache2/envvars

EXPOSE 80
EXPOSE 443
EXPOSE 10081
EXPOSE 10082

CMD ["/usr/local/bin/run"]
