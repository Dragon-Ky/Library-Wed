# Giai đoạn 1: Build bằng Maven sử dụng Amazon Corretto (rất ổn định)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# Copy file cấu hình và tải thư viện trước để tận dụng cache của Docker
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy toàn bộ code src và build ra file .jar
COPY src ./src
RUN mvn clean package -DskipTests

# Giai đoạn 2: Chạy ứng dụng (SỬA LỖI Ở ĐÂY)
# Thay openjdk bằng eclipse-temurin:17-jre-alpine (siêu nhẹ, chuyên cho Production)
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Copy file .jar từ giai đoạn build sang. 
# Lưu ý: *.jar giúp lấy đúng file dù tên project là gì
COPY --from=build /app/target/*.jar app.jar

# Mở cổng 8080 (cổng mặc định của Spring Boot)
EXPOSE 8080

# Chạy ứng dụng với giới hạn RAM để tránh bị Render Kill (vì gói Free chỉ có 512MB RAM)
ENTRYPOINT ["java", "-Xmx300m", "-Xss512k", "-jar", "app.jar"]