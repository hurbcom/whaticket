FROM node:14-alpine as build-deps
WORKDIR /usr/src/app

ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.1/dumb-init_1.2.1_amd64 /usr/local/bin/dumb-init
RUN chmod +x /usr/local/bin/dumb-init

# COPY package*.json ./
# RUN npm install
# COPY .env* ./
# COPY src/ ./src/
# COPY public/ ./public/
# RUN npm run build

COPY . ./
RUN npm install
RUN echo "REACT_APP_BACKEND_URL=http://whaticket-backend.stg.hucloud.com.br/" > .env
RUN npm run build

ENTRYPOINT ["dumb-init", "--"]
CMD node server.js

# FROM nginx:alpine
# RUN apk add --no-cache jq openssl

# ENV DOCKERIZE_VERSION v0.6.1
# RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
#     && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
#     && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# ENV PUBLIC_HTML=/var/www/public/

# COPY .docker/nginx /etc/nginx/
# COPY --from=build-deps /usr/src/app/build ${PUBLIC_HTML}
# EXPOSE 80

# COPY .docker/add-env-vars.sh /docker-entrypoint.d/01-add-env-vars.sh
# RUN chmod +x /docker-entrypoint.d/01-add-env-vars.sh
