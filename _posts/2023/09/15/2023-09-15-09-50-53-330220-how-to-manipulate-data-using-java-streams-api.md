---
layout: post
title: "How to manipulate data using Java Streams API"
description: " "
date: 2023-09-15
tags: [Streams]
comments: true
share: true
---

The Java Streams API was introduced in Java 8, offering a powerful way to manipulate collections of data. With Java Streams, you can perform various operations on data, such as filtering, mapping, sorting, and reducing, in a concise and functional way.

## Filtering Data

Filtering allows you to select elements from a collection that match a specific condition. You can use `filter()` method in Java Streams to achieve this.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

List<Integer> evenNumbers = numbers.stream()
                                   .filter(num -> num % 2 == 0)
                                   .collect(Collectors.toList());

// Output: [2, 4, 6, 8, 10]
System.out.println(evenNumbers);
```

## Mapping Data

Mapping allows you to transform or extract data from each element in a collection. You can use `map()` method in Java Streams to achieve this.

```java
List<String> names = Arrays.asList("John", "Jane", "Adam", "Eve");

List<String> upperCaseNames = names.stream()
                                   .map(String::toUpperCase)
                                   .collect(Collectors.toList());

// Output: [JOHN, JANE, ADAM, EVE]
System.out.println(upperCaseNames);
```

## Sorting Data

Sorting allows you to order elements in a collection based on a specific attribute. You can use `sorted()` method in Java Streams to achieve this.

```java
List<String> fruits = Arrays.asList("Apple", "Orange", "Banana", "Mango");

List<String> sortedFruits = fruits.stream()
                                 .sorted()
                                 .collect(Collectors.toList());

// Output: [Apple, Banana, Mango, Orange]
System.out.println(sortedFruits);
```

## Reducing Data

Reducing allows you to combine elements in a collection to produce a single result. You can use `reduce()` method in Java Streams to achieve this.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

int sum = numbers.stream()
                 .reduce(0, (a, b) -> a + b);

// Output: 15
System.out.println(sum);
```

## Conclusion

The Java Streams API provides a convenient way to manipulate data in a functional manner. With operations like filtering, mapping, sorting, and reducing, you can easily perform complex data manipulations using a concise syntax. Learning and mastering Java Streams can significantly contribute to writing cleaner and more efficient code.

#Java #Streams