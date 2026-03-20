# Stage 1: Build the application using Maven
FROM maven:3.9.8-eclipse-temurin-17 AS build
WORKDIR /app
# Copy the root pom and src
COPY pom.xml .
COPY api-gateway/ api-gateway/
COPY category-service/ category-service/
# Build the specific module
RUN mvn clean package -pl category-service -am -DskipTests

# Stage 2: Create the runtime image
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/category-service/target/*.jar app.jar
EXPOSE 8082
ENTRYPOINT ["java", "-jar", "app.jar"]
