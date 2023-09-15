---
layout: post
title: "Understanding intermediate and terminal operations in Java Streams API"
description: " "
date: 2023-09-15
tags: [java, streamapi]
comments: true
share: true
---

## Intermediate Operations
Intermediate operations are operations that can be performed on a stream and produce another stream as a result. These operations are *lazy*, meaning they are not executed immediately when they are called. Instead, they are *deferred* until a terminal operation is invoked on the stream.

Some common intermediate operations in the Java Streams API include:

### `filter(Predicate<T> predicate)`
This operation filters the stream based on a given predicate. It takes a predicate function as an argument and returns a new stream that contains only the elements that satisfy the predicate.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
Stream<Integer> evenNumbersStream = numbers.stream()
                                          .filter(number -> number % 2 == 0);
```

### `map(Function<T, R> mapper)`
The `map` operation transforms each element in the stream using a given function. It takes a function as an argument and returns a new stream containing the results of applying the function to each element.

```java
Stream<String> uppercasedStream = names.stream()
                                       .map(String::toUpperCase);
```

### `sorted(Comparator<T> comparator)`
This operation sorts the elements of the stream based on a given comparator. It takes a comparator as an argument and returns a new stream with the elements sorted accordingly.

```java
List<String> sortedNames = names.stream()
                               .sorted()
                               .collect(Collectors.toList());
```

## Terminal Operations
Terminal operations are operations that mark the end of a stream pipeline and produce a non-stream result. When a terminal operation is invoked, all intermediate operations in the pipeline are executed.

Some common terminal operations in the Java Streams API include:

### `collect(Collector<T, A, R> collector)`
The `collect` operation accumulates the elements of the stream into a collection or a single value. It takes a `Collector` instance as an argument, which defines how the stream elements should be collected.

```java
List<String> collectedNames = names.stream()
                                  .collect(Collectors.toList());
```

### `forEach(Consumer<T> action)`
This operation performs an action for each element in the stream. It takes a consumer function as an argument and applies it to each element sequentially.

```java
names.stream()
     .forEach(System.out::println);
```

### `reduce(BinaryOperator<T> accumulator)`
The `reduce` operation combines the elements of the stream into a single value. It takes a binary operator as an argument and performs a cumulative operation on the elements.

```java
Optional<Integer> sum = numbers.stream()
                               .reduce(Integer::sum);
```

In conclusion, intermediate operations in the Java Streams API are used to transform or filter the elements of a stream, while terminal operations produce a result or perform an action on the elements. Understanding these operations and their differences is crucial for effectively working with the streams API and writing clean and concise code.

#java #streamapi