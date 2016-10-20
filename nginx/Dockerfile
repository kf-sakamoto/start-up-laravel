FROM nginx:latest

MAINTAINER Fukuyama Nobukazu <fukuyama@kf-works.co.jp>

ADD nginx.conf /etc/nginx/
ADD laravel.conf /etc/nginx/conf.d/

RUN echo "upstream php-upstream { server php-fpm:9000; }" > /etc/nginx/conf.d/upstream.conf

EXPOSE 80 443

CMD ["nginx"]
