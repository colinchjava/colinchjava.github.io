---
layout: post
title: "CompletableFuture in Java 8"
description: " "
date: 2023-10-24
tags: [completablefuture]
comments: true
share: true
---

Java 8 introduced a new feature called CompletableFuture that allows you to write asynchronous and non-blocking code in a more straightforward and readable manner. In this blog post, we will explore the CompletableFuture class and see how it can be used in Java 8 to handle asynchronous tasks.

## Table of Contents
- [Introduction to CompletableFuture](#introduction-to-completablefuture)
- [Creating a CompletableFuture](#creating-a-completablefuture)
- [Chaining CompletableFuture](#chaining-completablefuture)
- [Exception Handling](#exception-handling)
- [Combining CompletableFutures](#combining-completablefutures)
- [Summary](#summary)

## Introduction to CompletableFuture

CompletableFuture is a class in the java.util.concurrent package that represents an asynchronous task that produces a result or completes exceptionally. It is similar to the Future interface but provides more flexibility and functionality.

The CompletableFuture class is designed to work with functional programming techniques, making it easier to compose asynchronous operations and chain them together.

## Creating a CompletableFuture

To create a CompletableFuture, you can use the static methods provided by the CompletableFuture class, such as `completedFuture`, `supplyAsync`, or `runAsync`. These methods are used to either create a completed CompletableFuture, execute a supplier asynchronously, or execute a runnable asynchronously, respectively.

Here is an example of how to create a CompletableFuture using the `supplyAsync` method:

```java
CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> {
    // Perform some long-running task
    return "Result";
});
```

In the above example, the `supplyAsync` method takes a supplier (a lambda expression) that will be executed asynchronously. The CompletableFuture is then returned and can be used to retrieve the result of the asynchronous task once it completes.

## Chaining CompletableFuture

One of the powerful features of CompletableFuture is the ability to chain multiple CompletableFuture instances together. This allows you to create a pipeline of asynchronous operations and specify how the results of one operation should be used as the input for the next operation.

You can chain CompletableFuture instances using methods like `thenApply`, `thenAccept`, and `thenCompose`. These methods are used to apply a function to the result of a CompletableFuture, consume the result of a CompletableFuture, or compose two CompletableFutures, respectively.

Here is an example of how to chain CompletableFuture instances using the `thenApply` method:

```java
CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> "Hello")
        .thenApply(s -> s + " World")
        .thenApply(String::toUpperCase);

String result = completableFuture.get();
System.out.println(result); // Output: HELLO WORLD
```

In the above example, the `thenApply` method is used to concatenate " World" to the result of the first CompletableFuture, and then convert the result to uppercase.

## Exception Handling

CompletableFuture provides methods to handle exceptions that occur during the execution of asynchronous tasks. You can use the `exceptionally` method to specify a fallback value or computation when the CompletableFuture completes exceptionally.

Here is an example of how to handle exceptions in CompletableFuture:

```java
CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> {
    // Perform some long-running task that may throw an exception
    throw new RuntimeException("Something went wrong");
}).exceptionally(ex -> "Fallback value");

String result = completableFuture.get();
System.out.println(result); // Output: Fallback value
```

In the above example, the `exceptionally` method is used to provide a fallback value when the CompletableFuture completes exceptionally.

## Combining CompletableFutures

CompletableFuture also provides methods to combine multiple CompletableFuture instances and wait for all of them to complete. These methods include `thenCombine`, `thenAcceptBoth`, and `allOf`.

Here is an example of how to combine multiple CompletableFuture instances using the `thenCombine` method:

```java
CompletableFuture<String> completableFuture1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> completableFuture2 = CompletableFuture.supplyAsync(() -> "World");

CompletableFuture<String> combinedFuture = completableFuture1.thenCombine(completableFuture2, (s1, s2) -> s1 + " " + s2);

String result = combinedFuture.get();
System.out.println(result); // Output: Hello World
```

In the above example, the `thenCombine` method is used to combine the results of two CompletableFutures by concatenating them together.

## Summary

CompletableFuture in Java 8 is a powerful tool for writing asynchronous and non-blocking code. It provides a wide range of methods to create, chain, handle exceptions, and combine CompletableFuture instances.

By leveraging CompletableFuture, you can simplify the process of handling asynchronous tasks and make your code more readable and maintainable.

Remember to import the `CompletableFuture` class from the `java.util.concurrent` package to start using its capabilities in your Java 8 projects.

**#java #completablefuture**