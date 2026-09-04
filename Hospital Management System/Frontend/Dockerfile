# Builder stage
FROM node:20 AS builder
WORKDIR /app

# Copy package files from the frontend folder (paths relative to repo root)
COPY ["Hospital Management System/Frontend/package.json", "Hospital Management System/Frontend/package-lock.json*", "./"]

RUN npm ci || npm install

# Copy the frontend source
COPY ["Hospital Management System/Frontend/", "./"]

# Build the Angular app
RUN npm run build -- --configuration production || npm run build

# Production image
FROM nginx:stable-alpine
RUN rm -rf /usr/share/nginx/html/*

# Copy built files (adjust path if your angular.json outputs to a different folder)
COPY --from=builder /app/dist/Frontend /usr/share/nginx/html

# Copy nginx config for SPA fallback
COPY ["Hospital Management System/Frontend/nginx.conf", "/etc/nginx/conf.d/default.conf"]

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
