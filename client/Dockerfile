FROM node:alpine as builder

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install

COPY ./ ./

RUN npm run build

FROM nginx:alpine

COPY nginx.conf /etc/nginx/nginx.conf

## Remove default nginx index page
RUN rm -rf /usr/share/nginx/html/*

COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 3000 80

CMD ["nginx", "-g", "daemon off;"]
