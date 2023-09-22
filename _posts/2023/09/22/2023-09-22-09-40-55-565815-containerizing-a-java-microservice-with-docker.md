---
layout: post
title: "Containerizing a Java microservice with Docker"
description: " "
date: 2023-09-22
tags: [Docker]
comments: true
share: true
---

In this blog post, we will discuss how to containerize a Java microservice using Docker. Containerization has become increasingly popular as it allows for easy deployment and scalability of applications. Docker, a widely-used container platform, provides a seamless way to package and distribute applications as containers.

## Prerequisites
Before we begin, make sure you have the following prerequisites in place:
1. Docker installed on your machine.
2. A Java microservice project with a `Dockerfile` already set up.

## Step 1: Build the Microservice
To containerize our Java microservice, we first need to build the project. Navigate to your microservice project directory and run the following command:

```
$ ./gradlew clean build
```

If you are using Maven, replace `./gradlew` with `./mvnw` in the above command.

## Step 2: Create a Dockerfile
Create a file called `Dockerfile` in the root directory of your project. Open the `Dockerfile` and add the following content:

```
# Use the official OpenJDK 11 base image
FROM openjdk:11-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the microservice JAR file into the container
COPY build/libs/microservice.jar .

# Expose the port the microservice will run on
EXPOSE 8080

# Set the command to run the microservice when the container starts
CMD ["java", "-jar", "microservice.jar"]
```

The `Dockerfile` above starts with an OpenJDK 11 base image, sets the working directory, copies the built JAR file into the container, exposes the microservice port, and sets the command to run the microservice.

## Step 3: Build the Docker Image
To build the Docker image, navigate to the project directory in your terminal and run the following command:

```
$ docker build -t my-microservice:1.0 .
```

Here, `my-microservice` is the image name, and `1.0` is the version tag. Adjust these values according to your preferences.

## Step 4: Run the Docker Container
Once the Docker image is built, you can run it as a container using the following command:

```
$ docker run -d -p 8080:8080 my-microservice:1.0
```

This command starts the Docker container in detached mode (`-d`), mapping the microservice port `8080` on the host to the same port inside the container.

## Conclusion
In this blog post, we have learned how to containerize a Java microservice using Docker. Docker provides an efficient way to package and deploy applications, making it easier to manage and scale your microservices. By following the steps outlined, you can successfully containerize and run your Java microservice in a Docker container.

#Java #Docker