---
layout: post
title: "How to handle null values in Java Streams API"
description: " "
date: 2023-09-15
tags: [Java, JavaStreams, NullValues]
comments: true
share: true
---

The Java Streams API introduced in Java 8 allows for concise and efficient data processing operations on collections. However, handling null values when using streams can be a bit tricky. In this blog post, we will explore different ways to handle null values when working with Java Streams.

## 1. Filter Null Values
To filter out null values from a stream, you can use the `filter()` method along with a null check condition. Here's an example:

```java
List<String> list = Arrays.asList("apple", null, "banana", null, "carrot");
List<String> resultList = list.stream()
                            .filter(Objects::nonNull)
                            .collect(Collectors.toList());
System.out.println(resultList);
// Output: [apple, banana, carrot]
```

In the code snippet above, the `filter()` method is used with the `Objects::nonNull` method reference, which checks if each element in the stream is not null.

## 2. Replace Null Values
In some cases, you may want to replace null values with a default value or a specific value. You can achieve this by using the `map()` method along with a null-checking lambda expression. Here's an example:

```java
List<String> list = Arrays.asList("apple", null, "banana", null, "carrot");
List<String> resultList = list.stream()
                            .map(s -> s != null ? s : "unknown")
                            .collect(Collectors.toList());
System.out.println(resultList);
// Output: [apple, unknown, banana, unknown, carrot]
```

In the code snippet above, the `map()` method is used with a lambda expression to check each element and replace any null values with the string "unknown".

## Conclusion
Handling null values when working with Java Streams API is essential to avoid potential `NullPointerExceptions`. By using the `filter()` method to remove null values or the `map()` method to replace them, you can ensure smooth data processing with streams.

#Java #JavaStreams #NullValues