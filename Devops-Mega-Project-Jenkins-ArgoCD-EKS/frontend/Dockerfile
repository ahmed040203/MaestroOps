# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

COPY .env.docker .env.production
RUN npm run build

# ------------------- Stage 2: Serve with nginx ------------------------------
FROM nginx:1.27-alpine

COPY --from=frontend-builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 5173

CMD ["nginx", "-g", "daemon off;"]
