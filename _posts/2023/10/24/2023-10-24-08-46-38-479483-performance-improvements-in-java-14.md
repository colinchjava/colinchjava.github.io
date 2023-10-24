---
layout: post
title: "Performance improvements in Java 14"
description: " "
date: 2023-10-24
tags: [Performance]
comments: true
share: true
---

Java 14, released in March 2020, brings several performance enhancements that can improve the execution speed and efficiency of Java applications. In this blog post, we will explore some of these key improvements and their impact on the performance of Java programs.

## 1. NUMA-Aware Memory Allocation

Non-Uniform Memory Access (NUMA) is a memory architecture that provides different memory access latencies depending on the location of the data in memory. Java 14 introduces NUMA-aware memory allocation, which improves the performance of Java applications running on NUMA hardware architectures.

By default, Java 14 uses an algorithm that detects the availability of NUMA hardware and allocates memory accordingly. This optimization reduces the latency and improves memory bandwidth, resulting in better performance for multi-threaded Java applications.

To enable NUMA-aware memory allocation, you can use the `XX:+UseNUMA` flag when starting the Java Virtual Machine (JVM).

## 2. ZGC Concurrent Class Unloading

Class unloading is a process in the JVM that removes classes from memory when they are no longer needed. In previous versions of Java, class unloading caused a stop-the-world pause, affecting the overall performance of the application.

With Java 14's Z Garbage Collector (ZGC), class unloading can now be performed concurrently, meaning that it no longer causes significant pauses in the application. This improvement can have a positive impact on the performance of long-running Java applications, especially those that dynamically load and unload classes.

To enable ZGC and take advantage of concurrent class unloading, you can use the `XX:+UseZGC` flag when starting the JVM.

## 3. JIT Compiler Improvements

Java 14 includes several improvements to its Just-In-Time (JIT) compiler, which is responsible for dynamically optimizing the bytecode of Java programs at runtime.

One notable improvement is the introduction of a new JIT compiler called "JEP 333: ZGC Parallel Memory Deallocation." This compiler is optimized for parallel memory deallocation and helps in reducing the overhead associated with memory deallocation operations.

Additionally, Java 14 introduces a new feature called "JEP 345: NUMA-Aware Memory Allocation for G1." This feature enhances the performance of the Garbage-First (G1) garbage collector on NUMA hardware architectures.

Combined, these JIT compiler improvements result in faster application startup times, reduced memory overhead, and improved overall performance for Java programs.

## Conclusion

Java 14 brings significant performance improvements that can benefit a wide range of Java applications. By leveraging NUMA-aware memory allocation, concurrent class unloading, and JIT compiler enhancements, developers can achieve better performance and efficiency in their Java programs.

It's worth noting that these improvements are just a fraction of the enhancements introduced in Java 14. To explore more features and improvements, be sure to check out the official documentation and release notes from Oracle.

# References
- [Java 14 Release Notes](https://www.oracle.com/java/technologies/javase/14u-relnotes.html)
- [JEP 345: NUMA-Aware Memory Allocation for G1](https://openjdk.java.net/jeps/345)
- [JEP 333: ZGC Parallel Memory Deallocation](https://openjdk.java.net/jeps/333)
- [Non-Uniform Memory Access (NUMA)](https://en.wikipedia.org/wiki/Non-uniform_memory_access)  #Java #Performance