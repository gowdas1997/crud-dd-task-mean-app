# Stage 1: Build Stage (Builder Pattern)
FROM node:18-alpine AS builder
WORKDIR /app
# Copy package files and install dependencies
COPY package*.json ./
RUN npm install
COPY . .

# Stage 2: Production Stage
FROM node:18-alpine
WORKDIR /app
# Copy built files from the builder stage
COPY --from=builder /app .
# Backend application runs on port 9090 (as per server.js)
EXPOSE 9090
# CRITICAL FIX: Run server.js directly using correct JSON array syntax
CMD [ "node", "server.js" ]
