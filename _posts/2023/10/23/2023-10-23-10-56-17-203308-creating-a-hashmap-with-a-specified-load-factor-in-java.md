---
layout: post
title: "Creating a HashMap with a specified load factor in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, the `HashMap` class provides an efficient way to store and retrieve key-value pairs. By default, it uses a load factor of `0.75`, which means that once the number of elements in the map exceeds `75%` of the initial capacity, the map will automatically be resized to maintain its performance.

However, there may be cases where we want to create a `HashMap` with a different load factor. Fortunately, Java provides a constructor that allows us to specify the load factor when creating a `HashMap`.

Here's an example of how to create a `HashMap` with a load factor of `0.5`:

```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        // Create a HashMap with a load factor of 0.5
        HashMap<String, Integer> map = new HashMap<>(16, 0.5f);

        // Add key-value pairs to the map
        map.put("Apple", 1);
        map.put("Banana", 2);
        map.put("Orange", 3);

        // Print the map
        System.out.println(map);
    }
}
```

In the above code, we use the `HashMap(int initialCapacity, float loadFactor)` constructor to create a `HashMap` object. The `initialCapacity` parameter specifies the initial capacity of the map, and the `loadFactor` parameter specifies the desired load factor.

By specifying a load factor of `0.5`, we indicate that the map should be resized once it reaches `50%` of its initial capacity. This can be useful if we know in advance that our map will contain a relatively small number of elements.

Please note that choosing a lower load factor may reduce the frequency of resizing operations, but it will also increase the memory usage of the `HashMap`. Therefore, it's important to strike a balance between performance and memory efficiency based on your specific use case.

By leveraging the ability to customize the load factor, you can optimize the performance of `HashMap` to better suit your needs in Java programming.

## References
- [HashMap documentation](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/HashMap.html)
- [Java 8 HashMap source code](https://hg.openjdk.java.net/jdk8/jdk8/jdk/file/tip/src/share/classes/java/util/HashMap.java)