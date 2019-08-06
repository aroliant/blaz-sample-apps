FROM node:10.15.0 as builder
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY ./package.json package-lock.json nginx.conf /usr/src/app/

RUN npm install

COPY ./ /usr/src/app

RUN npm run ng build -- --prod

FROM nginx:alpine

COPY --from=builder /usr/src/app/nginx.conf /etc/nginx/nginx.conf

WORKDIR /usr/share/nginx/html
COPY --from=builder /usr/src/app/dist/sample/ .