# STAGE 1: Build Stage
FROM node:20-alpine AS builder
RUN apk add --no-cache curl unzip
WORKDIR /app

RUN curl -L -o /tmp/cart.zip https://roboshop-artifacts.s3.amazonaws.com/cart-v3.zip && \
    unzip /tmp/cart.zip && \
    rm /tmp/cart.zip

RUN npm install --omit=dev


# STAGE 2: Run Stage (Final Slim Image)
FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app /app

ENV REDIS_HOST=redis \
    CATALOGUE_HOST=catalogue \
    CATALOGUE_PORT=8080

EXPOSE 8080

# Start the application
CMD ["node", "server.js"]