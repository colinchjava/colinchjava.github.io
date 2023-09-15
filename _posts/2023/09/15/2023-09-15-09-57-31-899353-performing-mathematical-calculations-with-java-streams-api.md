---
layout: post
title: "Performing mathematical calculations with Java Streams API"
description: " "
date: 2023-09-15
tags: []
comments: true
share: true
---

## Summing elements

One of the most basic mathematical calculations is summing the elements of a collection. With the Streams API, this can be achieved easily using the `sum()` method. Let's assume we have a list of integers and we want to find the sum of all the elements:

```java
import java.util.Arrays;
import java.util.List;

public class MathOperations {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        int sum = numbers.stream()
                .mapToInt(Integer::intValue)
                .sum();

        System.out.println("Sum: " + sum);
    }
}
```

Output:
```
Sum: 15
```

In the above example, we convert the Stream of `Integer` objects to an `IntStream` using the `mapToInt()` method, which allows us to use the `sum()` method.

## Finding minimum and maximum

The Streams API also provides convenient methods to find the minimum and maximum values in a collection. Let's consider a list of integers and find the minimum and maximum values:

```java
import java.util.Arrays;
import java.util.List;

public class MathOperations {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        int min = numbers.stream()
                .mapToInt(Integer::intValue)
                .min()
                .orElse(0);

        int max = numbers.stream()
                .mapToInt(Integer::intValue)
                .max()
                .orElse(0);

        System.out.println("Minimum: " + min);
        System.out.println("Maximum: " + max);
    }
}
```

Output:
```
Minimum: 1
Maximum: 5
```

In the above example, we use the `min()` and `max()` methods after converting the Stream of `Integer` objects to an `IntStream`. The `orElse()` method is used to handle the case where the Stream is empty.

## Calculating average

Calculating the average of a collection of numbers is another common mathematical operation. The Streams API provides the `average()` method to achieve this. Let's calculate the average of a list of integers:

```java
import java.util.Arrays;
import java.util.List;

public class MathOperations {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        double average = numbers.stream()
                .mapToInt(Integer::intValue)
                .average()
                .orElse(0);

        System.out.println("Average: " + average);
    }
}
```

Output:
```
Average: 3.0
```

In the above example, we use the `average()` method after converting the Stream of `Integer` objects to an `IntStream`. The `orElse()` method is used in case the Stream is empty.

In conclusion, the Java Streams API is not only useful for filtering and transforming data but also for performing common mathematical calculations. Whether you need to sum elements, find minimum and maximum values, or calculate averages, the Streams API provides a clean and concise way to perform these operations.