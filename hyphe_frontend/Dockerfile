FROM nginx:alpine

ENV NODE_ENV=propduction
COPY . /frontend/

WORKDIR /frontend

RUN apk --update add git nodejs \
    && npm install -g bower webpack \
    && npm install --production \
    && npm run build && bower install --allow-root \
    && npm uninstall -g bower webpack \
    && apk del git nodejs \ 
    && rm /var/cache/apk/*

COPY ./docker-nginx-vhost.conf /etc/nginx/conf.d/default.conf 

COPY docker-entrypoint.sh /

RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]
