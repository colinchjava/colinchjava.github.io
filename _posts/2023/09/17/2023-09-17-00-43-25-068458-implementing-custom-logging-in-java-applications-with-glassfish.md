---
layout: post
title: "Implementing custom logging in Java applications with GlassFish"
description: " "
date: 2023-09-17
tags: [glassfish, customlogging]
comments: true
share: true
---

In large-scale Java applications, logging is a crucial component for monitoring and troubleshooting. While GlassFish, an open-source application server, provides built-in logging functionality, you may encounter scenarios where custom logging is required.

In this blog post, we will explore how to implement custom logging in Java applications deployed on GlassFish. Following these steps, you will be able to configure your own logging mechanism according to your specific requirements.

## Step 1: Creating a Custom Logger Class

The first step is to create a custom logger class that extends the `java.util.logging.Logger` class. This allows you to override the logging methods and define your own logging behavior.

```java
import java.util.logging.Level;
import java.util.logging.Logger;

public class CustomLogger extends Logger {
    
    protected CustomLogger(String name, String resourceBundleName) {
        super(name, resourceBundleName);
    }
    
    public void customLog(Level level, String message) {
        // Custom logging implementation
    }
    
    // Override other logging methods as necessary
}
```

In the `customLog` method, you can define your own logic for logging the message at the specified level. You can write the logs to a file, a database, or any other target location.

## Step 2: Configuring GlassFish for Custom Logging

Next, you need to configure GlassFish to use your custom logger class. This can be achieved by modifying the `logging.properties` file located in the GlassFish installation directory.

Open the `logging.properties` file and locate the handler configuration section. Add the following line to register your custom logger:

```properties
handlers=com.example.CustomLoggerHandler
```

## Step 3: Creating Custom Logger Handler

Create a custom log handler class that implements the `java.util.logging.Handler` interface. This handler will receive log records from the GlassFish server and forward them to your custom logger.

```java
import java.util.logging.Handler;
import java.util.logging.LogRecord;

public class CustomLoggerHandler extends Handler {
    
    @Override
    public void publish(LogRecord record) {
        CustomLogger logger = CustomLogger.getLogger(record.getLoggerName());
        logger.customLog(record.getLevel(), record.getMessage());
    }
    
    @Override
    public void flush() {
        // Implementation for flushing
    }
    
    @Override
    public void close() {
        // Implementation for closing
    }
}
```

In the `publish` method, you can retrieve the custom logger based on the logger name from the log record. Then, you can invoke the custom logging method to process the log record.

## Step 4: Deploying the Custom Logger

To deploy the custom logger with your Java application on GlassFish, you need to package the custom logger classes along with your application. You can create a JAR file containing the custom logger classes and include it in your application's classpath.

After deploying your application, GlassFish will use your custom logger for logging, as configured in the `logging.properties` file.

Going forward, you can expand on this foundation and enhance the custom logger class and log handler according to your application's logging requirements.

Implementing custom logging in Java applications allows you to have more control over the log output and integration with external logging systems. With GlassFish, the process of configuring and deploying custom logging is straightforward, providing you with a powerful tool for application monitoring and debugging.

#glassfish #customlogging