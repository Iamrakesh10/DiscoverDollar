# Stage 1 - Build Angular
FROM node:18 AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build --prod

# Stage 2 - Serve Angular with Nginx
FROM nginx:alpine

# Copy our custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy the Angular dist folder
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80
