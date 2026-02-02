# ---------- build stage ----------
FROM node:20-alpine AS builder

WORKDIR /app

# copy ทั้ง project ก่อน (สำคัญ)
COPY . .

# install dependencies
RUN npm ci

# build quasar
RUN npm run build


# ---------- production stage ----------
FROM nginx:alpine

# ลบ config default
RUN rm /etc/nginx/conf.d/default.conf

# copy build output
COPY --from=builder /app/dist/spa /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
