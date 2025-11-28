# Stage 1: Build Angular app
FROM node:18 as build

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build --prod

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy Angular build
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# Copy NGINX reverse proxy config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
