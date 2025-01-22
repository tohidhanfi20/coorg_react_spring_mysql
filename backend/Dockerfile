# Step 1: Build the Spring Boot application
FROM openjdk:17-jdk-slim AS build

# Install Maven
RUN apt-get update && apt-get install -y maven && apt-get clean

# Set the working directory
WORKDIR /app

# Copy pom.xml and install dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code
COPY src ./src

# Build the Spring Boot application
RUN mvn clean package -DskipTests

# Step 2: Run the Spring Boot application
FROM openjdk:17-jdk-slim

# Copy the JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose port for Spring Boot app
EXPOSE 8081

# Command to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "/app.jar"]
