FROM alpine:latest AS build-stage
WORKDIR /app
COPY . .

FROM nginx:stable-alpine
# Explicitly setting root, though it is the default in this image
USER root
RUN rm -rf /usr/share/nginx/html/*
COPY --from=build-stage /app/frontend-v3 /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]