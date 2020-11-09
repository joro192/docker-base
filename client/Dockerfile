# Stage 0, "build-stage", based on Node.js, to build and compile the frontend
FROM node:10-alpine as build-stage

RUN mkdir -p /app
WORKDIR /app

COPY package.json /app
COPY yarn.lock /app
COPY . /app

RUN yarn install && yarn build

# Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
FROM nginx:alpine

COPY --from=build-stage /app/build /var/www

COPY --from=build-stage nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

ENTRYPOINT ["nginx","-g","daemon off;"]