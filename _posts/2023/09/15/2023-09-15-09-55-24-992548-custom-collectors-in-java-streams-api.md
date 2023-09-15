---
layout: post
title: "Custom collectors in Java Streams API"
description: " "
date: 2023-09-15
tags: [Java, StreamsAPI, CustomCollectors]
comments: true
share: true
---

Java Streams API introduced in Java 8 provides a powerful way to process and manipulate data. It allows developers to write expressive and functional code for data transformation and aggregation. One of the key features of Streams API is the ability to perform operations in a parallel manner, making it efficient for handling large datasets.

Collectors in Java Streams API provide a convenient way to accumulate elements from a stream into a collection or perform a reduction operation. While Java provides several built-in collectors like `toList()`, `toSet()`, and `joining()`, there may be scenarios where you need to create your own custom collectors to meet specific requirements.

## Implementing a Custom Collector

To create a custom collector, you need to implement the `Collector` interface, which consists of four methods:

1. `supplier()`: This method returns a supplier function that creates an empty accumulator for collecting elements.
2. `accumulator()`: This method returns a function that performs the element accumulation.
3. `combiner()`: This method returns a function that performs a reduction operation for merging multiple accumulators into a single accumulator.
4. `finisher()`: This method returns a function that performs the final transformation of the accumulated result.

Let's look at an example of a custom collector that collects the distinct elements from a stream into a `LinkedHashSet`:

```java
import java.util.*;
import java.util.stream.Collector;
import java.util.stream.Collectors;

public class DistinctCollector<T> implements Collector<T, Set<T>, Set<T>> {
    @Override
    public Supplier<Set<T>> supplier() {
        return LinkedHashSet::new;
    }

    @Override
    public BiConsumer<Set<T>, T> accumulator() {
        return Set::add;
    }

    @Override
    public BinaryOperator<Set<T>> combiner() {
        return (set1, set2) -> {
            set1.addAll(set2);
            return set1;
        };
    }

    @Override
    public Function<Set<T>, Set<T>> finisher() {
        return Function.identity();
    }

    @Override
    public Set<Characteristics> characteristics() {
        return Collections.emptySet();
    }
}

// Usage example
List<String> words = Arrays.asList("hello", "world", "hello", "java", "hello");
Set<String> distinctWords = words.stream().collect(new DistinctCollector<>());
```

In the above example, we implemented the `Collector` interface for collecting distinct elements into a `LinkedHashSet`. The `supplier()` method returns a supplier that creates a new `LinkedHashSet`, the `accumulator()` method adds elements to the set, the `combiner()` method merges two sets, the `finisher()` method returns the accumulated set, and the `characteristics()` method returns an empty set of characteristics.

## Conclusion

Custom collectors in Java Streams API provide a way to extend the functionality of built-in collectors to meet specific requirements. By implementing the `Collector` interface, you can create collectors that perform complex grouping, filtering, or reduction operations. Custom collectors help in writing more expressive and reusable code while leveraging the power and parallel processing capabilities of the Streams API.

#Java #StreamsAPI #CustomCollectors