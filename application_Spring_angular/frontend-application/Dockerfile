### STAGE 1: Build ###
FROM node:16-alpine AS build 
WORKDIR /app
COPY . .
RUN npm install --force

ARG configuration=production
RUN npm run build -- --output-path=./dist/frontend-application  --configuration $configuration

### STAGE 2: Run ###
FROM nginx:alpine
COPY --from=build /app/dist/frontend-application /usr/share/nginx/html
COPY /nginx-custom.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]


