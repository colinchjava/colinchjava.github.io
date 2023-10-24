---
layout: post
title: "Java 9 process API improvements"
description: " "
date: 2023-10-24
tags: [ProcessAPIImprovements]
comments: true
share: true
---

Java 9 introduced several enhancements to the Process API, making it more powerful and flexible for managing and interacting with operating system processes. In this blog post, we'll explore some of the key improvements in the Process API.

## Table of Contents
- [Introduction](#introduction)
- [New Methods in the Process API](#new-methods-in-the-process-api)
- [Process Info](#process-info)
- [Managing Processes with Streams](#managing-processes-with-streams)
- [Conclusion](#conclusion)

## Introduction
In previous versions of Java, managing processes and interacting with system commands was a somewhat cumbersome task. However, in Java 9, the Process API has been enhanced with new methods to ease the handling of external processes.

## New Methods in the Process API
Java 9 introduced three new methods in the `java.lang.Process` class:

1. `isAlive()`: This method returns a boolean value indicating whether the subprocess associated with the `Process` object is still running.

2. `pid()`: The `pid()` method returns the process identifier of the subprocess. This is particularly useful when you need to obtain the process ID of a running process.

3. `destroyForcibly()`: The `destroyForcibly()` method forcefully terminates the subprocess represented by the `Process` object. This can be used when you want to forcibly stop a process.

## Process Info
With Java 9, you can now retrieve information about the operating system process without resorting to native code. The new `ProcessHandle` interface provides methods to get process information such as process ID, parent process, command used to launch the process, and more.

```java
ProcessHandle currentProcess = ProcessHandle.current();
long processId = currentProcess.pid();
System.out.println("Current Process ID: " + processId);

Optional<ProcessHandle> parentProcess = currentProcess.parent();
parentProcess.ifPresentOrElse(
    parent -> System.out.println("Parent Process ID: " + parent.pid()),
    () -> System.out.println("Parent process not available.")
);
```

## Managing Processes with Streams
Java 9 introduced the `ProcessBuilder` class, which allows you to easily build and manage processes with a more streamlined and functional approach. The `ProcessBuilder` class provides methods to redirect input, output, and error streams. It also provides the ability to chain the process execution using streams.

```java
ProcessBuilder processBuilder = new ProcessBuilder("ls", "-l");

try {
    Process process = processBuilder.start();

    // Read output from the process
    BufferedReader reader = new BufferedReader(new InputStreamReader(process.getInputStream()));
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }

    // Wait for the process to complete
    int exitCode = process.waitFor();
    System.out.println("Process exited with code " + exitCode);
} catch (IOException | InterruptedException e) {
    // Handle exception
}
```

## Conclusion
The improvements in the Java 9 Process API make it easier to work with external processes, retrieve process information, and manage the execution of processes. These enhancements provide a more robust and flexible approach to process management in Java.

These enhancements enable developers to effectively interact with operating system processes, making Java a more powerful language for system-level programming.

# References
- [Java SE 9: JEP 102 - Process API Updates](https://openjdk.java.net/jeps/102) 
- [Java Platform, Standard Edition Oracle JDK 9 Documentation: Class Process](https://docs.oracle.com/javase/9/docs/api/java/lang/Process.html)
- [Java Platform, Standard Edition Oracle JDK 9 Documentation: Interface ProcessHandle](https://docs.oracle.com/javase/9/docs/api/java/lang/System.html) 

#hashtags: #Java #ProcessAPIImprovements