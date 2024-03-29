# Use a base image with necessary tools for building the application
FROM alpine:latest AS builder

# Install necessary dependencies (e.g., git) for the build process
RUN apk update && apk add --no-cache git

# Set the working directory in the container
WORKDIR /app

# Clone the repository from the context
COPY . .

# Build the application using Dockerfile.multi
RUN docker build -t my-petclinic-image -f Dockerfile.multi .

# Start a new stage for the final image
FROM openjdk:8-jdk-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the built artifacts from the previous stage
COPY --from=builder /app/target/*.jar app.jar

# Expose the port the application runs on
EXPOSE 8080

# Specify the command to run the service
CMD ["java", "-jar", "app.jar"]
