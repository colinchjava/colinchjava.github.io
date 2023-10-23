---
layout: post
title: "Creating an unmodifiable HashMap in Java"
description: " "
date: 2023-10-23
tags: [References, unmodifiableMap]
comments: true
share: true
---

In Java, a `HashMap` is a commonly used data structure that allows you to store key-value pairs. By default, a `HashMap` is modifiable, which means you can add, remove, and modify its entries. However, there may be scenarios where you want to create a `HashMap` that is unmodifiable, meaning its contents cannot be changed once it is created. In this blog post, we will explore how to create an unmodifiable `HashMap` in Java.

## Using Collections.unmodifiableMap()

Java provides the `Collections` utility class, which includes a method called `unmodifiableMap()` that allows you to create an unmodifiable view of a `Map` instance. Here's an example of how to use it:

```java
import java.util.HashMap;
import java.util.Collections;
import java.util.Map;

public class UnmodifiableHashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("orange", 3);

        Map<String, Integer> unmodifiableMap = Collections.unmodifiableMap(map);
        
        // Trying to modify the unmodifiableMap will throw an UnsupportedOperationException
        unmodifiableMap.put("grape", 4); // Throws UnsupportedOperationException
    }
}
```
In the example above, we first create a `HashMap` called `map` and populate it with some key-value pairs. Then, we use the `Collections.unmodifiableMap()` method to create an unmodifiable view of `map` and assign it to the `unmodifiableMap` variable. Finally, we try to add a new entry to the `unmodifiableMap`, which results in an `UnsupportedOperationException` being thrown.

## Benefits of using an unmodifiable HashMap

Using an unmodifiable `HashMap` has several benefits:

1. **Immutable data**: The unmodifiable `HashMap` ensures that once created, its contents cannot be modified. This can be helpful in scenarios where you want to guarantee that the data remains unaltered throughout the program execution.

2. **Thread-safe**: Since an unmodifiable `HashMap` cannot be modified, it is inherently thread-safe. This means that multiple threads can safely access and read the contents of the `HashMap` without the need for explicit synchronization.

3. **Security**: In certain cases, you may want to pass a `HashMap` to another component of your program without allowing it to modify the contents. By creating an unmodifiable `HashMap`, you can ensure that the other component can only read the data and cannot make any unwanted changes.

In conclusion, creating an unmodifiable `HashMap` in Java can be done using the `Collections.unmodifiableMap()` method. It provides immutability, thread-safety, and security benefits for scenarios where you want to ensure that the contents of the `HashMap` cannot be modified.

#References:
- [Java Collections API documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collections.html#unmodifiableMap(java.util.Map))