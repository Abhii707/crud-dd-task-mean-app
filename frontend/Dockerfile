# ---- Build Angular ----
FROM node:20-alpine AS build
WORKDIR /app


COPY frontend/package*.json ./
RUN npm ci


COPY frontend ./
# Build prod bundle (adjust if your script differs)
RUN npm run build -- --configuration production


# ---- Serve with Nginx + Reverse Proxy to backend ----
FROM nginx:1.27-alpine
# Copy built Angular app (replace <dist-folder> with your actual dist dir name under /app/dist)
COPY --from=build /app/dist /usr/share/nginx/html


# Replace default Nginx config with our reverse proxy config
COPY deploy/nginx/nginx.conf /etc/nginx/nginx.conf


EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]