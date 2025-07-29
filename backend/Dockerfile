# Stage 1: Build the application
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: Production image with minimal footprint
FROM node:18-alpine
WORKDIR /app
# Only copy built assets and production dependencies
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm ci --production  # Install only production dependencies
CMD ["node", "dist/server.js"]  # Run the built application
