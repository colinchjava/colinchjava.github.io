---
layout: post
title: "Managing environment variables in Java Docker containers"
description: " "
date: 2023-09-22
tags: [docker]
comments: true
share: true
---

![docker-logo](https://cdn.iconscout.com/icon/free/png-256/docker-226091.png)

Environment variables are an essential part of configuring and managing applications running in Docker containers. They provide a flexible way to store and access configuration values without hardcoding them in the codebase. In this blog post, we will discuss how to manage environment variables in Java Docker containers.

## Why use environment variables?

Environment variables allow us to separate application configuration from the codebase, making it easier to manage different deployment environments (e.g., development, staging, production). By using environment variables, we can easily change configuration values without the need to rebuild or redeploy the container.

## Setting environment variables in Docker

There are multiple ways to set environment variables in Docker containers. One common approach is to use the `-e` flag when running the `docker run` command. For example:

```
docker run -e "ENV_VAR_NAME=value" image_name
```

This command sets the value of `ENV_VAR_NAME` to `value` inside the container. You can set multiple environment variables by specifying the `-e` flag multiple times.

## Managing environment variables in Java

To access environment variables in Java, we can use the `System.getenv("ENV_VAR_NAME")` method. This method retrieves the value of the specified environment variable.

Here's an example of how to access and use environment variables in a Java application:

```java
public class AppConfig {
    private String databaseUrl;
    private String apiKey;

    public AppConfig() {
        this.databaseUrl = System.getenv("DATABASE_URL");
        this.apiKey = System.getenv("API_KEY");
    }

    // Getter methods...
}
```

In this example, the `AppConfig` class retrieves the values of `DATABASE_URL` and `API_KEY` environment variables during object creation. These values can then be used to initialize and configure application components.

## Managing environment variables with Docker Compose

[Docker Compose](https://docs.docker.com/compose/) is a tool for defining and running multi-container Docker applications. It provides a convenient way to manage environment variables through a dedicated configuration file.

Here's an example of how to define environment variables in a Docker Compose file:

```yaml
version: "3"
services:
  myapp:
    image: myapp-image
    environment:
      - DATABASE_URL=${DATABASE_URL}
      - API_KEY=${API_KEY}
```

In this example, we define two environment variables (`DATABASE_URL` and `API_KEY`) for the `myapp` service. The values of these variables can be provided through the host environment or an `.env` file.

## Conclusion

Managing environment variables is crucial for configuring and deploying Java applications in Docker containers. By separating application configuration from the codebase, we can easily adapt our applications to different environments and change configuration values without rebuilding or redeploying the containers. Docker provides multiple ways to set environment variables, and Java provides a simple way to access them. Docker Compose offers a convenient solution for managing environment variables across multiple services.

#docker #java #environmentvariables #dockercompose