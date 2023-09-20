---
layout: post
title: "Logging messages to different log files based on severity in Java"
description: " "
date: 2023-09-20
tags: [Logging]
comments: true
share: true
---

Logging is an essential part of any software application, as it helps in debugging, troubleshooting, and monitoring the application's behavior. In some cases, it is beneficial to log messages to different log files based on their severity levels. This allows us to easily filter and analyze logs based on the level of importance.

In this blog post, we will explore how to implement logging messages to different log files based on severity in Java using the popular logging framework, Log4j 2.

## What is Log4j 2?

Log4j 2 is a powerful and extensively configurable logging framework for Java applications. It provides various logging levels such as DEBUG, INFO, WARN, ERROR, and FATAL, allowing us to categorize messages based on their severity.

To get started, we need to include the Log4j 2 dependency in our project. You can add the following Maven dependency to your pom.xml file:

```xml
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
    <version>2.14.1</version>
</dependency>
```

## Configuration

Log4j 2 uses a configuration file to define the loggers, appenders, and log levels. Let's create a sample configuration file named `log4j2.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
    <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
        </Console>
        
        <RollingFile name="ErrorFile" fileName="logs/error.log" filePattern="logs/error-%d{MM-dd-yyyy}.log">
            <ThresholdFilter level="ERROR" onMatch="ACCEPT" onMismatch="DENY"/>
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
            <Policies>
                <OnStartupTriggeringPolicy />
            </Policies>
        </RollingFile>
        
        <RollingFile name="InfoFile" fileName="logs/info.log" filePattern="logs/info-%d{MM-dd-yyyy}.log">
            <ThresholdFilter level="INFO" onMatch="ACCEPT" onMismatch="DENY"/>
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
            <Policies>
                <OnStartupTriggeringPolicy />
            </Policies>
        </RollingFile>
    </Appenders>
    <Loggers>
        <Root level="DEBUG">
            <AppenderRef ref="Console" />
            <AppenderRef ref="ErrorFile" />
            <AppenderRef ref="InfoFile" />
        </Root>
    </Loggers>
</Configuration>
```

In this configuration file, we have defined three appenders: Console, ErrorFile, and InfoFile. The Console appender logs all messages to the console, while the ErrorFile and InfoFile appenders log messages with severity levels ERROR and INFO respectively to separate log files.

The `fileName` attribute specifies the path and name of the log file, and the `filePattern` attribute defines the pattern for rolling log files based on the current date.

## Logging Messages

To log messages using Log4j 2, we need to create a `Logger` object and use its various log methods. Here's an example:

```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

public class MyApp {
    private static final Logger logger = LogManager.getLogger(MyApp.class);

    public static void main(String[] args) {
        logger.debug("This is a debug message.");
        logger.info("This is an info message.");
        logger.warn("This is a warning message.");
        logger.error("This is an error message.");
        logger.fatal("This is a fatal message.");
    }
}
```

In this example, we have created a logger for the `MyApp` class using the `LogManager.getLogger()` method. We can then use the logger's methods like `debug()`, `info()`, `warn()`, `error()`, and `fatal()` to log messages with different severity levels.

When we run the above code, Log4j 2 will log the messages to the console and the respective log files based on their severity levels as defined in the configuration file.

## Conclusion

Logging messages to different log files based on severity is a useful technique that allows us to effectively manage and analyze logs. Log4j 2 provides a flexible and powerful logging framework to implement this functionality in Java applications. By using Log4j 2's configuration file, we can easily define separate appenders for different log files and control the log levels.

Implementing this approach can significantly streamline the process of troubleshooting and debugging your applications, and help you gain insights into the behavior of your software.

## #Java #Logging