
#Build Steps

FROM node:12.2.0-alpine as build
USER root

WORKDIR /app

COPY . /app/


RUN npm config set unsafe-perm true
RUN npm install
RUN npm install react-scripts@5.0.1 -g --silent

RUN npm run build

#Run Steps
FROM nginx:1.19.8-alpine  
USER root
#FROM nginxinc/nginx-unprivileged
COPY --from=build /app/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d
#COPY nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
