---
layout: post
title: "Observability and monitoring options for Shenandoah GC in Java"
description: " "
date: 2023-10-10
tags: [observability, monitoring]
comments: true
share: true
---

## Introduction
Shenandoah is a garbage collector (GC) algorithm for Java that aims to minimize GC pause times and improve the responsiveness of applications. It is designed to operate with low-latency, making it suitable for applications with large heaps and strict performance requirements. In this blog post, we will explore the observability and monitoring options available for Shenandoah GC in Java.

## Enabling Shenandoah GC
To use Shenandoah GC in your Java application, you need to enable it with the following JVM options:

```
-Xmx<heapSize> -XX:+UnlockExperimentalVMOptions -XX:+UseShenandoahGC
```

Replace `<heapSize>` with the desired size of the Java heap.

## Logging Shenandoah Events
Shenandoah GC generates events that provide insights into its behavior and performance. You can enable event logging by adding the following JVM option:

```
-XX:+UnlockDiagnosticVMOptions -XX:+LogShenandoahGC
```

This option directs the Shenandoah GC events to the standard output. You can redirect the output to a log file by using standard shell redirection.

## Visualizing Shenandoah GC Events with GCViewer
GCViewer is a popular tool for analyzing and visualizing GC logs. You can use GCViewer to parse and visualize the Shenandoah GC events logged to a file. To use GCViewer, simply download the latest release from its GitHub repository and run the following command:

```
java -jar gcviewer.jar <logFile>
```

Replace `<logFile>` with the path to your Shenandoah GC log file. GCViewer will display comprehensive graphs and statistics to help you understand the behavior of Shenandoah GC.

## Monitoring Shenandoah GC with Java Mission Control
Java Mission Control (JMC) is a powerful monitoring and profiling tool provided by Oracle. It offers various functionalities for monitoring and profiling Java applications, including built-in support for monitoring the GC. To monitor Shenandoah GC using JMC, follow these steps:

1. Start your Java application with Shenandoah GC enabled.
2. Launch JMC and connect it to your running Java application.
3. Navigate to the "VM Information" tab in JMC.
4. Under the "Garbage Collectors" section, you will find metrics related to Shenandoah GC, such as pause times, throughput, and memory utilization.

JMC provides a real-time view of various metrics related to Shenandoah GC, allowing you to monitor and assess the performance of your application.

## Conclusion
Observability and monitoring are crucial for understanding and optimizing the behavior of the Shenandoah GC algorithm in Java applications. By enabling event logging and leveraging tools like GCViewer and Java Mission Control, you can gain valuable insights into the performance of Shenandoah GC and make informed decisions to optimize your application's memory management.

#observability #monitoring