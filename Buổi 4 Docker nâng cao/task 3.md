## Task 2. Yêu cầu
```sh
- Cho source code của ứng dụng https://github.com/handuy/angular-hero
- Viết Dockerfile dưới dạng multi-stage, sau đó build ứng dụng thành Docker Image và khởi tạo container.
```
### - Dockerfile:
```sh
FROM node:13-alpine as build-step
RUN apk add --update --no-cache \
      autoconf \
      libtool \
      automake \
      nasm \
      gcc \
      make \
      g++ \
      zlib-dev \
      tzdata \
      build-base
      
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:1.17-alpine
COPY --from=build-step /app/dist /usr/share/nginx/html
EXPOSE 8081
CMD ["nginx", "-g", "daemon off;"]
```
### - Build image:
```sh
docker build -t angular-app .
```
### - Run container:
```sh
docker run --name angular1 -d -p 8081:80 angular-app
```