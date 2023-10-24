---
layout: post
title: "Enhancements to Streams API in Java 9"
description: " "
date: 2023-10-24
tags: [stream]
comments: true
share: true
---

Java 9 introduced several enhancements to the Streams API, which is a powerful functional programming feature introduced in Java 8. These enhancements provide developers with more flexibility and ease when working with streams. In this blog post, we will explore some of the important enhancements introduced in Java 9.

## 1. Stream API Improvements

### Improved `takeWhile` and `dropWhile` Methods

In Java 9, the Stream API now includes two new methods - `takeWhile` and `dropWhile`. These methods allow you to take or drop elements from a stream based on a specific condition until the condition is no longer met.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

List<Integer> takenNumbers = numbers.stream()
    .takeWhile(n -> n < 5)
    .collect(Collectors.toList());
// takenNumbers will contain [1, 2, 3, 4]

List<Integer> droppedNumbers = numbers.stream()
    .dropWhile(n -> n < 5)
    .collect(Collectors.toList());
// droppedNumbers will contain [5, 6, 7, 8, 9, 10]
```

### `ofNullable` Method

Java 9 introduced the `ofNullable` method to the `Stream` interface. This method allows you to create a stream with a single element, which can be nullable. This is useful when you want to include a null value in a stream.

```java
String name = "John";
Stream<String> stream = Stream.ofNullable(name);
// If `name` is not null, stream will contain a single element (i.e., "John")
// If `name` is null, stream will be empty
```

## 2. Optional Improvements

### `ifPresentOrElse` Method

Java 9 introduced the `ifPresentOrElse` method to the `Optional` class. This method allows you to specify two different actions to be performed based on whether the optional value is present or not.

```java
Optional<String> optionalName = Optional.ofNullable("John");

optionalName.ifPresentOrElse(
    name -> System.out.println("Hello, " + name),
    () -> System.out.println("No name provided")
);
// Output: Hello, John

Optional<String> emptyOptional = Optional.empty();

emptyOptional.ifPresentOrElse(
    name -> System.out.println("Hello, " + name),
    () -> System.out.println("No name provided")
);
// Output: No name provided
```

## Conclusion

The enhancements introduced to the Streams API and Optional class in Java 9 provide developers with more flexibility and control when working with streams and optional values. These improvements simplify common tasks and make the code more expressive and concise. Make sure to check out the Java 9 documentation for more details on these enhancements.

\#java #stream-api