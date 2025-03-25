# ใช้ OpenJDK 21 เป็น Base Image
FROM openjdk:21-jdk-slim

# ตั้งค่า Working Directory เป็น /app
WORKDIR /app

# คัดลอกไฟล์โปรเจกต์ทั้งหมดจาก backend ไปยัง container
COPY . /app

# แก้ปัญหา CRLF (Windows Line Endings) ในไฟล์ `mvnw`
RUN sed -i 's/\r$//' mvnw && chmod +x mvnw
RUN chmod +x wait-for-it.sh

# ดาวน์โหลด Dependencies ล่วงหน้า เพื่อลดเวลา Build
RUN ./mvnw dependency:resolve

# คอมไพล์และแพ็กเกจเป็น JAR ไฟล์
RUN ./mvnw package -DskipTests

# ใช้ JAR ไฟล์ที่สร้างเป็น Entry Point
CMD ./wait-for-it.sh my-mysql:3306 -- java -jar target/transport-application-0.0.1-SNAPSHOT.jar