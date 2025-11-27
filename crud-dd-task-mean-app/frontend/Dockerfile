# Stage 1: Build Angular App (Node.js environment)
FROM node:18-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
# Run Angular production build
RUN npm run build -- --output-path=./dist --configuration=production

# Stage 2: Serve the built app with Nginx
FROM nginx:alpine
# CRITICAL FIX: Copy the built Angular files from the build stage using the correct output path 'dist/angular-15-crud'
COPY --from=build /app/dist /usr/share/nginx/html
# Nginx default port inside the container is 80
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
