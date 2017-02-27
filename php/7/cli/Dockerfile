FROM php:7-alpine
	
RUN apk update && apk add --no-cache git zip nodejs

RUN npm install -g bower webpack

RUN apk add --no-cache --virtual .yarn-deps curl gnupg && \
  curl -o- -L https://yarnpkg.com/install.sh | sh && \
  apk del .yarn-deps && ln -s /root/.yarn/bin/yarn /usr/bin/yarn

RUN apk add --no-cache --virtual .php-deps libmcrypt-dev && \
	docker-php-ext-install mcrypt && \
	apk del .php-deps

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	# && php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
	&& php composer-setup.php \
	&& php -r "unlink('composer-setup.php');" \
	&& mv composer.phar /usr/bin/composer

WORKDIR /src/app

VOLUME /src/app

CMD ["/bin/sh"]