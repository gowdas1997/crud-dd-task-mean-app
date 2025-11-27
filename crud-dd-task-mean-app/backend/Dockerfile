# Stage 1: Build Stage (Optional but good for efficiency)
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

# Stage 2: Production Stage
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app .
# MongoDB connection URL should be passed as an environment variable in docker-compose.yml
# The default port for Node/Express is 3000
EXPOSE 3000
CMD [ "npm", "start" ]
