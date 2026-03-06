# Giai đoạn 1: Build bằng Maven
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# Giai đoạn 2: Chạy ứng dụng (SỬA Ở ĐÂY)
# Thay vì openjdk:17-jdk-slim, hãy dùng eclipse-temurin:17-jre-alpine cho nhẹ và ổn định
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# Copy file .jar đã build từ Giai đoạn 1 sang
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]