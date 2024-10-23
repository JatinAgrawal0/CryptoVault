# Step 1: Use a Maven image to build the project
FROM maven:3.9.2-eclipse-temurin-17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the pom.xml and download the dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the entire project into the container (src and other files)
COPY src ./src

# Build the project
RUN mvn clean package -DskipTests

# Step 2: Use a minimal JDK image to run the application
FROM eclipse-temurin:17-jdk-jammy

# Set the working directory inside the container
WORKDIR /app

# Copy the jar file from the build stage to the current stage
COPY --from=build /app/target/treading-plateform-0.0.1-SNAPSHOT.jar app.jar

# Expose the port your app runs on
EXPOSE 8080

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
