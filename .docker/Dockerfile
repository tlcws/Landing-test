FROM php:7.4-apache 
RUN docker-php-ext-install mysqli
RUN a2enmod rewrite

RUN apt-get update && \
    apt-get install --no-install-recommends --assume-yes --quiet ca-certificates curl git && \
    rm -rf /var/lib/apt/lists/*

RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -

COPY php.ini /usr/local/etc/php/conf.d

RUN sed -i 's/Options -Indexes/Options +Indexes/g' /etc/apache2/conf-available/docker-php.conf

ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' > /usr/local/etc/php/php.ini