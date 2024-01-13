FROM ubuntu:20.04

WORKDIR /app
COPY . .

RUN apt-get update && \
    apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt update
RUN apt install -y php7.4 \
                   php7.4-fpm \
                   php7.4-zip \
                   php7.4-mbstring \
                   php7.4-tokenizer \
                   php7.4-mysql \
                   php7.4-gd \
                   php7.4-xml \
                   php7.4-bcmath \
                   php7.4-intl \
                   php7.4-curl
RUN apt install -y nodejs
RUN apt install -y composer
RUN apt install -y npm
RUN composer install
RUN npm install

# Variáveis da base de dados
ENV DB_HOST=mysql
ENV DB_DATABASE=swap
ENV DB_USERNAME=swap
ENV DB_PASSWORD=123456

# Variáveis do migrate e do seed
ENV MIGRATE=false
ENV SEED=false

# Preenchimento do .env
RUN sed -i 's/DB_HOST=127.0.0.1/DB_HOST=$DB_HOST/g' .env.example
RUN sed -i 's/DB_DATABASE=homestead/DB_DATABASE=$DB_DATABASE/g' .env.example
RUN sed -i 's/DB_USERNAME=homestead/DB_USERNAME=$DB_USERNAME/g' .env.example
RUN sed -i 's/DB_PASSWORD=secret/DB_PASSWORD=$DB_PASSWORD/g' .env.example
RUN mv .env.example .env

RUN php artisan key:generate

EXPOSE 8000

RUN chmod +x ./script.sh
CMD ./script.sh
