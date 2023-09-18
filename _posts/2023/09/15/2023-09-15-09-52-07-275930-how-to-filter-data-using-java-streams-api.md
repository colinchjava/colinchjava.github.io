---
layout: post
title: "How to filter data using Java Streams API"
description: " "
date: 2023-09-15
tags: [StreamsAPI]
comments: true
share: true
---

The Java Streams API provides a powerful way to work with collections of data. Filtering data is one of the most common operations performed on a collection. With the Streams API, you can easily filter data based on certain conditions, making your code concise and readable.

To filter data using Java Streams API, follow these steps:

1. Convert your collection into a stream: You can convert any collection such as List or Set into a stream by calling the `stream()` method.

```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5);
Stream<Integer> numberStream = numbers.stream(); 
```

2. Use the `filter()` method: The `filter()` method allows you to specify a predicate, which is a boolean-valued function that tests each element in the stream. Only the elements that satisfy the predicate will be included in the resulting stream.

```java
Stream<Integer> filteredStream = numberStream.filter(number -> number % 2 == 0);
```

In this example, the `filter()` method is used with a lambda expression to filter out all the odd numbers from the stream.

3. Perform an operation on the filtered stream: After filtering the data, you can perform various operations on the filtered stream, such as mapping, sorting, or collecting the data.

```java
List<Integer> evenNumbers = filteredStream.collect(Collectors.toList());
```

In this example, the `collect()` method is used to collect the filtered stream into a new list.

4. Complete the stream: It's important to close the stream once you're done with it, to release any resources associated with it.

```java
numberStream.close();
```

Here, the `close()` method is called to close the original stream.

By following these steps, you can easily filter data using the Java Streams API. This approach provides a clean and efficient way to work with collections and perform filtering operations.

#Java #StreamsAPI