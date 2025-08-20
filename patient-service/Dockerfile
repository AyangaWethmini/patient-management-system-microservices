# Stage 1: Build
FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

# Copy pom.xml first to leverage caching
COPY pom.xml .

# Download dependencies (optional but speeds up builds)
RUN mvn dependency:go-offline -B

# Copy source code
COPY src ./src

# Package the Spring Boot app
RUN mvn clean package -DskipTests

# Stage 2: Run
FROM openjdk:21-jdk AS runner

WORKDIR /app

# Copy jar from builder
COPY --from=builder /app/target/patient-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4000

ENTRYPOINT ["java", "-jar", "app.jar"]
