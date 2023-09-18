---
layout: post
title: "Manipulating streams of data using Java Stream wrapper class"
description: " "
date: 2023-09-14
tags: [Streams]
comments: true
share: true
---

![Java Stream Logo](https://example.com/stream_logo.png) 

Java's Stream API provides a powerful way to process and manipulate data in a declarative and functional style. It allows developers to perform various operations on streams of data, such as filtering, mapping, and reducing, with ease. In this blog post, we will explore how to manipulate streams of data using the Java Stream wrapper class.

## Introduction to Java Stream

In Java, a Stream is a sequence of elements that can be processed in parallel or sequentially. It does not store data but rather carries the data from a source (such as a collection or an I/O channel) through a pipeline of intermediate and terminal operations.

## Creating a Stream

To manipulate streams of data, we need a stream source. We can create a stream from various sources like collections, arrays, or I/O channels. Once we have a stream, we can then apply various operations on it.

Let's consider an example where we have a list of names and we want to filter out the names starting with the letter 'A'.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

public class StreamExample {

    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Alex");
        names.add("Charlie");

        Stream<String> filteredNames = names.stream()
                .filter(name -> name.startsWith("A"));

        filteredNames.forEach(System.out::println);
    }
}
```

In the above code, we create a list of names and use the `stream()` method to create a stream from the list. Then we use the `filter()` method to filter out the names starting with 'A'. Finally, we use the `forEach()` method to print the filtered names.

## Common Operations on Streams

### Filtering

One of the most common operations on streams is filtering. It allows us to select only the elements that match a given condition. For example, we can filter out the even numbers from a stream of integers.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenNumbers = numbers.stream()
        .filter(number -> number % 2 == 0);

evenNumbers.forEach(System.out::println);
```

In the above code, we create a list of numbers and use the `filter()` method to filter out the even numbers. Finally, we use the `forEach()` method to print the even numbers.

### Mapping

Mapping is another common operation on streams that allows us to transform the elements of a stream. We can apply a function on each element and get a new stream with the transformed elements. For example, we can convert a stream of strings to a stream of their lengths.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

Stream<Integer> nameLengths = names.stream()
        .map(String::length);

nameLengths.forEach(System.out::println);
```

In the above code, we create a list of names and use the `map()` method to convert the names to their lengths. Finally, we use the `forEach()` method to print the lengths.

### Reducing

Reducing is an operation that combines all the elements of a stream into a single value. For example, we can get the sum of all the numbers in a stream.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

int sum = numbers.stream()
        .reduce(0, Integer::sum);

System.out.println("Sum: " + sum);
```

In the above code, we create a list of numbers and use the `reduce()` method to calculate the sum of the numbers. Finally, we print the sum.

## Conclusion

The Java Stream API provides a convenient and concise way to manipulate streams of data. In this blog post, we discussed the basics of working with streams and explored common operations like filtering, mapping, and reducing. By mastering the Java Stream API, you can write code that is more readable, maintainable, and efficient.

Happy coding!

#Java #Streams