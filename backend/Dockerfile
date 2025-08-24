# ---- Runtime (simple, fast) ----
FROM node:20-alpine
WORKDIR /usr/src/app


# Install only production deps first for layer caching
COPY backend/package*.json ./
RUN npm ci --omit=dev


# Copy source
COPY backend ./


ENV NODE_ENV=production \
  PORT=3000


# Make sure your server binds to 0.0.0.0 and reads MONGO_URI from env
EXPOSE 3000
CMD ["node", "server.js"]