FROM nginx:1.16.0-alpine

# cf.: https://github.com/jwilder/dockerize#for-alpine-images
RUN apk add --no-cache openssl=1.1.1b-r1

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

COPY default.tmpl /etc/nginx/conf.d/default.tmpl

CMD ["dockerize", "-template", "/etc/nginx/conf.d/default.tmpl:/etc/nginx/conf.d/default.conf", "-stdout", "/var/log/nginx/access.log", "-stderr", "/var/log/nginx/error.log", "nginx"]