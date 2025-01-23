# Step 1: Build the Spring Boot application using Maven
FROM maven:3.8-openjdk-17 AS build

# Set the working directory
WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# List files in /app to verify that the pom.xml is there
RUN ls -l /app

# Copy the source code
COPY src ./src

# List files in /app/src to verify the src folder is copied
RUN ls -l /app/src

# Build the Spring Boot application (use install instead of package for full build)
RUN mvn clean install -DskipTests -X  # Enable debug output

# Verify that the JAR file is in the target directory
RUN ls -l /app/target

# Step 2: Run the Spring Boot application
FROM openjdk:17-jdk-slim

# Copy the JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose port for the Spring Boot application
EXPOSE 8081

# Command to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "/app.jar"]
