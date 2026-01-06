# frontend/Dockerfile
############################
# Stage 1: Build the app
############################
FROM node:18-alpine AS builder
LABEL org.opencontainers.image.description="shopNow frontend - build stage"
WORKDIR /app

# Install build deps if needed
RUN apk add --no-cache python3 make g++ || true

# Copy package files (leverage cache)
COPY package*.json ./
RUN npm install --no-audit --prefer-offline

# Copy source and build
COPY . .

ENV REACT_APP_API_BASE_URL=/aryan/api
ENV PUBLIC_URL=/aryan

RUN npm run build

############################
# Stage 2: Runtime (nginx)
############################
FROM nginx:1.24-alpine
LABEL org.opencontainers.image.maintainer="you@example.com"

# Copy nginx config from build context
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy built static files from builder
COPY --from=builder /app/build /usr/share/nginx/html

# Expose web port
EXPOSE 80

# Run nginx in foreground
CMD ["nginx", "-g", "daemon off;"]

