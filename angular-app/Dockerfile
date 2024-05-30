# Stage 1: Build Angular application
FROM node:14 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build --prod

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/dist/angular-app /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
