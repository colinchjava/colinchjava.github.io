---
layout: post
title: "Creating immutable collections with Java Streams API"
description: " "
date: 2023-09-15
tags: [immutablecollections, javastreams]
comments: true
share: true
---

The Java Streams API provides a powerful and concise way to process collections of data. In addition to its functionality for data processing, it's also possible to create immutable collections using the Streams API. In this article, we will explore how to create immutable collections using the Java Streams API.

## Immutable List

To create an immutable list using the Java Streams API, you can use the `collect` method with the `Collectors.toList()` collector. The `collect` method allows you to accumulate the elements of a stream into a collection. Here's an example:

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class ImmutableCollectionExample {
    public static void main(String[] args) {
        List<Integer> numbers = Stream.of(1, 2, 3, 4, 5)
                .collect(Collectors.toList());

        // Attempting to modify the list will result in an UnsupportedOperationException
        numbers.add(6);  // Throws UnsupportedOperationException
    }
}
```

In the above example, we create an immutable list `numbers` by collecting the elements of a stream into a list using the `Collectors.toList()` collector. Since the list is immutable, any attempt to modify it, such as adding an element, will result in an `UnsupportedOperationException`.

## Immutable Set

Similarly, you can create an immutable set using the Java Streams API by using the `collect` method with the `Collectors.toSet()` collector. Here's an example:

```java
import java.util.Set;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class ImmutableCollectionExample {
    public static void main(String[] args) {
        Set<String> fruits = Stream.of("apple", "banana", "orange")
                .collect(Collectors.toSet());

        // Attempting to modify the set will result in an UnsupportedOperationException
        fruits.add("mango");  // Throws UnsupportedOperationException
    }
}
```

In the above example, we use the `Collectors.toSet()` collector to collect the elements of a stream into an immutable set `fruits`. As with the immutable list example, any attempt to modify the set will result in an `UnsupportedOperationException`.

## Conclusion

The Java Streams API provides a convenient way to create immutable collections. By using the `collect` method with appropriate collectors such as `Collectors.toList()` and `Collectors.toSet()`, you can easily create immutable lists and sets. Immutable collections offer advantages in terms of thread-safety, security, and easy debugging.

#immutablecollections #javastreams