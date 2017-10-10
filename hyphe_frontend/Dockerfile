FROM nginx:alpine

ENV NODE_ENV=production

COPY . /frontend/

WORKDIR /frontend

RUN apk --update add git nodejs \
    && npm install -g bower webpack \
    && npm install --production \
    && npm run build && bower install --allow-root \
    && bower --allow-root cache clean \
    && npm uninstall -g bower webpack \
    && npm cache clean \
    && apk del git nodejs \ 
    && rm -fr node_modules \
    && rm /var/cache/apk/*

COPY ./docker-nginx-vhost.conf /etc/nginx/conf.d/default.conf 

COPY docker-entrypoint.sh /

RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]
