FROM debian:11
LABEL maintainer="KOT_docker_lab1"

ENV TZ=Europe/Moscow

RUN printf "deb http://mirror.corbina.net/debian/ bullseye main non-free" > /etc/apt/sources.list.d/corbina.list

RUN apt-get update && apt-get upgrade &&\
apt install -y nginx &&\
rm -rf /var/lib/apt/lists/* &&\
apt clean &&\
rm -rf /var/www/* &&\
mkdir -p /var/www/labdocker.com/img &&\
echo "\ndaemon off;" >> /etc/nginx/nginx.conf

COPY index.html /var/www/labdocker.com/
COPY img.jpg /var/www/labdocker.com/img/

RUN useradd  kir &&\
groupadd nik &&\
usermod -a -G nik kir

RUN chmod -R 754 /var/www/labdocker.com &&\
chown -R kir:nik /var/www/labdocker.com 

RUN sed -i 's|/var/www/html|/var/www/labdocker.com|'g /etc/nginx/sites-enabled/default &&\
sed -i 's|www-data|kir|g' /etc/nginx/nginx.conf

CMD ["nginx"]
