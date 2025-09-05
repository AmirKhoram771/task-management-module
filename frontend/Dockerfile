# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Runtime (Nginx for serving)
FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html


CMD ["nginx", "-g", "daemon off;"]
