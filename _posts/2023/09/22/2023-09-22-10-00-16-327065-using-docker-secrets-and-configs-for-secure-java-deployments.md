---
layout: post
title: "Using Docker Secrets and Configs for secure Java deployments"
description: " "
date: 2023-09-22
tags: [technology, docker]
comments: true
share: true
---

In today's highly interconnected world, securing applications and sensitive data has become more important than ever. Docker, the popular containerization platform, provides us with powerful tools like Docker Secrets and Configs to help secure our applications.

In this blog post, we will explore how to use Docker Secrets and Configs to secure Java deployments. We will also provide examples of how to implement these features in your Java applications.

## Docker Secrets

Docker Secrets is a built-in feature that allows you to securely store sensitive information such as passwords, API keys, and certificates. Secrets are encrypted and only accessible by the Docker daemon and the container that needs to use them. Let's see how we can leverage Docker Secrets to secure a Java application.

1. **Create a Secret**

   First, we need to create a Docker Secret. Execute the following command on your Docker host:

   ```shell
   $ echo "mysecretpassword" | docker secret create db_password -
   ```

   Here, we are creating a secret named `db_password` with the value of `mysecretpassword`. The `-` sign at the end indicates that the secret value should be read from the standard input.

2. **Use the Secret in Java Application**

   Next, we need to modify our Java application to use the secret. We can access the secret value through an environment variable inside the container.

   ```java
   import java.util.Optional;

   public class MyApp {
       public static void main(String[] args) {
           String dbPassword = Optional.ofNullable(System.getenv("DB_PASSWORD"))
                                      .orElse("defaultpassword");

           // Use the dbPassword in your application
       }
   }
   ```

   In this example, we are using the `System.getenv()` method to retrieve the value of the environment variable `DB_PASSWORD`. If the environment variable is not set, we fallback to a default password.

3. **Deploy the Java Application with Docker**

   Finally, we need to deploy our Java application with Docker, ensuring that the secret is made available as an environment variable inside the container.

   ```dockerfile
   FROM openjdk:11

   ARG DB_PASSWORD_SECRET

   ENV DB_PASSWORD=$DB_PASSWORD_SECRET

   COPY target/myapp.jar /app.jar

   CMD ["java", "-jar", "/app.jar"]
   ```

   Here, we are passing the secret value as a build argument (`DB_PASSWORD_SECRET`) and setting it as an environment variable (`DB_PASSWORD`) in the container. The value will be accessible by our Java application.

## Docker Configs

Docker Configs is another powerful feature that allows you to manage application configurations. Unlike Docker Secrets, which are meant for sensitive information, Docker Configs are used for non-sensitive data such as application settings, database URLs, or external service endpoints. Let's see how we can use Docker Configs in a Java application.

1. **Create a Config**

   Similar to creating a Docker Secret, we can create a Docker Config. Execute the following command on your Docker host:

   ```shell
   $ echo "jdbc:mysql://localhost:3306/mydb" | docker config create db_url -
   ```

   Here, we are creating a config named `db_url` with the value of `jdbc:mysql://localhost:3306/mydb`.

2. **Use the Config in Java Application**

   Similar to using Docker Secrets, we can access the config value through an environment variable inside the container.

   ```java
   import java.util.Optional;

   public class MyApp {
       public static void main(String[] args) {
           String dbUrl = Optional.ofNullable(System.getenv("DB_URL"))
                                  .orElse("defaulturl");

           // Use the dbUrl in your application
       }
   }
   ```

   Here, we are retrieving the value of the environment variable `DB_URL` and falling back to a default URL if it is not set.

3. **Deploy the Java Application with Docker**

   Modify your Dockerfile to include the config in your Java application:

   ```dockerfile
   FROM openjdk:11

   ARG DB_URL_CONFIG

   ENV DB_URL=$DB_URL_CONFIG

   COPY target/myapp.jar /app.jar

   CMD ["java", "-jar", "/app.jar"]
   ```

   Here, we are passing the config value as a build argument (`DB_URL_CONFIG`) and setting it as an environment variable (`DB_URL`) in the container.

With Docker Secrets and Configs, you can effectively secure your Java deployments by separating sensitive information and non-sensitive configurations from your application code. This provides an extra layer of security and reduces the risk of exposing critical data.

#technology #docker #security