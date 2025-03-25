FROM node:20-alpine

# ตั้งค่า path การทำงานใน container
WORKDIR /app

# คัดลอกไฟล์ package.json และ package-lock.json ไปยัง container
COPY package*.json ./

# ติดตั้ง dependencies
RUN npm install

# คัดลอกไฟล์โปรเจกต์ทั้งหมดไปยัง container
COPY . .

# สร้างแอป Vue.js สำหรับ production
RUN npm run build

# ตั้งพอร์ตที่ container จะใช้
EXPOSE 5173

# รันแอปพลิเคชันในโหมด production ด้วย Vite preview
CMD ["npm", "run", "preview"]