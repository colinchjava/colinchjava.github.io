---
layout: post
title: "Using streams with HashMap in Java 8"
description: " "
date: 2023-10-23
tags: [stream]
comments: true
share: true
---

In Java 8, the introduction of the Stream API has made it easier to perform complex operations on collections. One useful feature is the ability to use streams with HashMaps. In this blog post, we will explore how to leverage streams to perform various operations on a HashMap in Java 8.

## Table of Contents
- [Filtering HashMap using Streams](#filtering-hashmap-using-streams)
- [Iterating over HashMap using Streams](#iterating-over-hashmap-using-streams)
- [Mapping HashMap using Streams](#mapping-hashmap-using-streams)
- [Conclusion](#conclusion)

## Filtering HashMap using Streams

With streams, filtering a HashMap based on certain conditions becomes effortless. Let's say we have a HashMap of employees' names and ages:

```java
HashMap<String, Integer> employees = new HashMap<>();
employees.put("John", 25);
employees.put("Jane", 30);
employees.put("Alex", 35);
employees.put("Emily", 28);
```

To filter this HashMap and get a new HashMap containing only the employees aged 30 and above, we can use the `filter` method of streams:

```java
HashMap<String, Integer> filteredEmployees = employees.entrySet()
    .stream()
    .filter(entry -> entry.getValue() >= 30)
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

In the above code, we convert the HashMap into a stream of key-value pairs using `entrySet()`. Then, we apply the `filter` method to check if the age is 30 or above. Finally, we use the `collect` method to convert the filtered stream back into a HashMap.

## Iterating over HashMap using Streams

Streams provide a concise way to iterate over a HashMap in Java 8. Suppose we want to print all the employees and their ages. We can achieve this using the `forEach` method of streams:

```java
employees.entrySet()
    .stream()
    .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));
```

Here, `forEach` iterates over each key-value pair in the HashMap and prints it to the console.

## Mapping HashMap using Streams

Streams also allow us to transform the values in a HashMap using the `map` method. Consider a scenario where we want to increase the age of each employee by 5 years:

```java
HashMap<String, Integer> updatedAges = employees.entrySet()
    .stream()
    .map(entry -> new AbstractMap.SimpleEntry<>(entry.getKey(), entry.getValue() + 5))
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

In the above code, we use the `map` method to create a new stream where each value is increased by 5. We create a new `AbstractMap.SimpleEntry` object with the updated age and collect it back into a new HashMap.

## Conclusion

Using streams with HashMaps in Java 8 provides a powerful way to manipulate and process collections. We've seen how to filter, iterate, and map a HashMap to perform various operations efficiently. By leveraging the Stream API, we can write clean and concise code that takes advantage of functional programming concepts.

Remember, if you are using Java 8 or above, utilizing streams with HashMaps can greatly enhance your code's readability and maintainability.

**#java #stream-api**