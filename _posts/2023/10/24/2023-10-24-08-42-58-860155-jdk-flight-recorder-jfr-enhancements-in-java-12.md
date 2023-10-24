---
layout: post
title: "JDK Flight Recorder (JFR) enhancements in Java 12"
description: " "
date: 2023-10-24
tags: [GUID]
comments: true
share: true
---

The JDK Flight Recorder (JFR) is a powerful tool for gathering profiling and diagnostic data from running Java applications. With Java 12, several enhancements have been introduced to further improve the capabilities and usability of JFR. In this blog post, we will explore these enhancements and see how they can benefit developers and operations teams.

## 1. Continuous recording

In previous versions of Java, JFR recordings were limited to a fixed duration. However, with Java 12, continuous recording is now supported. This means that JFR can continuously record events for an extended duration without the need to manually start and stop recordings. This is especially useful in scenarios where long-running applications need to be monitored over an extended period of time.

To enable continuous recording, simply use the `-XX:StartFlightRecording` flag with the `duration=0` parameter. For example:

```java
java -XX:StartFlightRecording:duration=0 -jar myapp.jar
```

## 2. Streaming data

Java 12 introduces the ability to stream JFR data to external systems in real-time. This allows for seamless integration with monitoring or analysis tools that require live data from running applications. The JFR streaming API provides a way to programmatically consume JFR data as it is generated.

To enable streaming, you can use the `-XX:StartFlightRecording` flag with the `settings=default` and `dumponexit=true` parameters. For example:

```java
java -XX:StartFlightRecording:settings=default,dumponexit=true -jar myapp.jar
```

You can then create a custom consumer by implementing the `jdk.jfr.consumer.EventStream` interface to receive and process the streaming data.

## Conclusion

The JDK Flight Recorder (JFR) enhancements in Java 12 provide developers and operations teams with powerful new features for profiling and monitoring Java applications. The continuous recording and streaming capabilities make it easier to gather and analyze data in real-time, leading to faster troubleshooting and performance optimization. Take advantage of these enhancements to improve the observability of your Java applications.

**References:**

- [JEP 328: Flight Recorder](https://openjdk.java.net/jeps/328)
- [Java Flight Recorder (JFR) Guide](https://docs.oracle.com/en/java/javase/12/troubleshoot/diagnostic-tools.html#GUID-EDF02AA2-E165-4273-BB3B-173A4E5A90F4)