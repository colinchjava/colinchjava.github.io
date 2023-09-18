---
layout: post
title: "Extracting and modifying data with Java Streams API"
description: " "
date: 2023-09-15
tags: [streamsapi]
comments: true
share: true
---

The Java Streams API introduced in Java 8 provides a powerful set of functions for working with collections of data in a functional programming style. With streams, we can easily extract and modify data using a concise and expressive syntax. In this blog post, we will explore some common operations for extracting and modifying data using the Java Streams API.

## Filtering Data

Filtering is a common operation when working with data. The Streams API provides the `filter` method to extract elements from a stream based on a given condition. Here's an example:

```java
List<String> names = Arrays.asList("John", "Jane", "Bob", "Alice", "Alex");

List<String> filteredNames = names.stream()
                                 .filter(name -> name.length() > 3)
                                 .collect(Collectors.toList());

System.out.println(filteredNames); // Output: [John, Jane, Alice]
```
In the above example, we create a stream from the `names` list and filter out the names that have a length less than or equal to 3. The filtered names are then collected into a new list.

## Mapping Data

Mapping is another frequently used operation to transform or modify elements in a stream. The Streams API provides the `map` method to apply a function to each element of a stream and obtain a new stream with the transformed elements. Here's an example:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<Integer> squaredNumbers = numbers.stream()
                                      .map(number -> number * number)
                                      .collect(Collectors.toList());

System.out.println(squaredNumbers); // Output: [1, 4, 9, 16, 25]
```

In the above example, we square each number in the `numbers` list and collect the squared numbers into a new list.

## Sorting Data

Sorting is another common operation that allows us to rearrange elements in a specific order. The Streams API provides the `sorted` method to sort the elements of a stream based on a given comparator. Here's an example:

```java
List<Integer> numbers = Arrays.asList(5, 2, 8, 3, 1);

List<Integer> sortedNumbers = numbers.stream()
                                      .sorted()
                                      .collect(Collectors.toList());

System.out.println(sortedNumbers); // Output: [1, 2, 3, 5, 8]
```

In the above example, we sort the elements in the `numbers` list in ascending order and collect the sorted numbers into a new list.

## Conclusion

The Java Streams API offers a powerful and expressive way to extract and modify data from collections. With operations like filtering, mapping, and sorting, we can easily manipulate data using a functional style. By leveraging the Java Streams API, developers can write cleaner and more concise code. Start exploring the streams API today and take advantage of its capabilities in your Java projects.

#java #streamsapi