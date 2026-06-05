# # Comment
# FROM node:24

# WORKDIR /app

# COPY package*.json ./

# RUN npm i 


# COPY . .

# RUN npm run build

# EXPOSE 3000

# CMD ["npm", "start"]

# Stage 1: Build
FROM node:24 as builder
WORKDIR /app
COPY package*.json ./
RUN npm i
COPY . .
RUN npm run build

# Stage 2: Production (c1)
# FROM node:24

# COPY --from=builder /app/.next /production/.next

# COPY --from=builder /app/package.json /production/package.json

# COPY --from=builder /app/node_modules /production/node_modules

# COPY --from=builder /app/public /production/public

# WORKDIR /production

# EXPOSE 3000

# CMD ["npm", "start"]
# Stage 2: Bàn ăn (Production)
FROM node:24-alpine AS runner
WORKDIR /app

# 1. Chỉ copy folder public (nếu web bạn có hình ảnh)
COPY --from=builder /app/public ./public

# 2. Copy folder .next/static (chứa CSS và JS của client)
COPY --from=builder /app/.next/static ./.next/static

# 3. Cú chốt: Copy toàn bộ thư mục standalone đã được lọc sẵn
COPY --from=builder /app/.next/standalone ./

# Mở cổng
EXPOSE 3000

# 4. Đổi lệnh chạy. Không dùng "npm start" nữa vì ta đã có file server.js trong standalone
CMD ["node", "server.js"]