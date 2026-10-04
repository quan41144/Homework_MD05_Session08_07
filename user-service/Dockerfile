# ==========================================================================
# Dockerfile Multi-stage build cho Spring Boot application
# ==========================================================================

# Giai đoạn 1 (builder): Sử dụng gradle:8.5-jdk17-alpine để biên dịch dự án ra file .jar
FROM gradle:8.5-jdk17-alpine AS builder
WORKDIR /app

# Copy toàn bộ source code vào container
COPY . .

# Biên dịch dự án ra file .jar
RUN gradle bootJar --no-daemon

# Giai đoạn 2 (production): Sử dụng eclipse-temurin:17-jre-alpine siêu nhẹ để chạy ứng dụng
FROM eclipse-temurin:17-jre-alpine AS production
WORKDIR /app

# Copy file .jar đã biên dịch từ stage builder sang stage production
COPY --from=builder /app/build/libs/*.jar app.jar

# Khai báo cổng 8080 theo yêu cầu
EXPOSE 8080

# Lệnh khởi chạy ứng dụng Spring Boot
ENTRYPOINT ["java", "-jar", "app.jar"]