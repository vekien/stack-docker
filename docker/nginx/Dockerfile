FROM nginx:1.19.3-alpine

#
# Copy project
#
WORKDIR  /var/www
COPY    ./project .

#
# Settings
#
ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#
# Copy config
#
COPY ./docker/nginx/site.conf  /etc/nginx/sites-enabled/default.conf
COPY ./docker/nginx/nginx.conf /etc/nginx/nginx.conf

#
# Finish
#
EXPOSE 80
