# Step 1: Build the Spring Boot application
FROM maven:3.8-openjdk-17 AS build

# Set the working directory
WORKDIR /app

# Copy pom.xml and install dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code
COPY src ./src

# Build the Spring Boot application
RUN mvn clean package -DskipTests

# List the contents of /app/target to verify where the JAR file is located
RUN ls -l /app/target

# Step 2: Run the Spring Boot application
FROM openjdk:17-jdk-slim

# Copy the JAR file from the build stage
# Adjust the path here based on the output from `ls -l /app/target`
COPY --from=build /app/target/*.jar app.jar

# Expose port for Spring Boot app
EXPOSE 8081

# Command to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "/app.jar"]
