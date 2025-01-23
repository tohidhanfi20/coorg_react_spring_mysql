# Step 1: Build the Spring Boot application using Maven
FROM maven:3.8-openjdk-17 AS build

# Set the working directory
WORKDIR /app

# Copy pom.xml and download dependencies (go offline to cache them)
COPY pom.xml .
RUN mvn dependency:go-offline

# List files in /app to verify that the pom.xml is there
RUN ls -l /app

# Copy the source code
COPY src ./src

# List files in /app/src to verify that the src folder is copied
RUN ls -l /app/src

# Build the application (use install instead of package for full build)
RUN mvn clean install -DskipTests -X  # Enable debug output

# Step 2: Run the Spring Boot application
FROM openjdk:17-jdk-slim

# Copy the JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose port for the Spring Boot application
EXPOSE 8081

# Command to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "/app.jar"]
