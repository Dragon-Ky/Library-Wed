# Giai đoạn 1: Build bằng Maven
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
# Copy file cấu hình và tải thư viện trước để cache
COPY pom.xml .
RUN mvn dependency:go-offline
# Copy code và build ra file .jar
COPY src ./src
RUN mvn clean package -DskipTests

# Giai đoạn 2: Chạy ứng dụng với JRE nhẹ
FROM openjdk:17-jdk-slim
WORKDIR /app
# Copy file .jar đã build từ Giai đoạn 1 sang
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]