# Stage 1: Build Angular App
FROM node:18-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
# The production build output is usually placed in a 'dist' folder
RUN npm run build -- --output-path=./dist --configuration=production

# Stage 2: Serve the built app with Nginx
FROM nginx:alpine
# Copy the built Angular files from the build stage to Nginx's public directory
COPY --from=build /app/dist/frontend /usr/share/nginx/html
# Nginx default port
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
