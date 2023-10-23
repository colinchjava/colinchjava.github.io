---
layout: post
title: "Creating a bidirectional HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, the `HashMap` class provides a convenient way to associate keys with values. However, it does not support bidirectional mapping, meaning that you can't easily look up a value based on a key or a key based on a value. In some scenarios, such as when you need to perform reverse lookups frequently, a bidirectional HashMap would be useful.

To create a bidirectional HashMap in Java, you can make use of two separate HashMap objects in combination:

1. One HashMap to store the key-value pairs in the normal way.
2. Another HashMap to store the value-key pairs, effectively allowing reverse lookups.

Here's an example implementation of a bidirectional HashMap in Java:

```java
import java.util.HashMap;
import java.util.Map;

public class BidirectionalHashMap<K, V> {
    private Map<K, V> forwardMap;
    private Map<V, K> reverseMap;

    public BidirectionalHashMap() {
        forwardMap = new HashMap<>();
        reverseMap = new HashMap<>();
    }

    public void put(K key, V value) {
        forwardMap.put(key, value);
        reverseMap.put(value, key);
    }

    public V get(K key) {
        return forwardMap.get(key);
    }

    public K reverseGet(V value) {
        return reverseMap.get(value);
    }

    // Additional methods such as remove, size, etc.
}
```

In the above example, we create a `BidirectionalHashMap` class that uses two separate HashMap objects, `forwardMap` and `reverseMap`, to store the key-value and value-key pairs respectively. The `put` method adds entries to both maps, while the `get` method retrieves values based on keys and the `reverseGet` method retrieves keys based on values.

You can utilize the bidirectional HashMap as follows:

```java
BidirectionalHashMap<String, Integer> map = new BidirectionalHashMap<>();
map.put("One", 1);
map.put("Two", 2);
map.put("Three", 3);

System.out.println(map.get("One")); // Output: 1
System.out.println(map.reverseGet(2)); // Output: Two
```

By using a bidirectional HashMap, you can easily perform reverse lookups in Java without the need for additional data structures or complex logic.

Remember to import the necessary packages and modify the class and data types based on your specific requirements.

# Conclusion

With the help of two HashMap objects, you can create a bidirectional HashMap in Java that allows for efficient reverse lookups. This can be particularly useful in scenarios where you need to retrieve keys based on values frequently. By implementing this simple solution, you can enhance the flexibility and usability of your Java applications.

References:
- [Java HashMap documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html)
- [Java Generics documentation](https://docs.oracle.com/javase/tutorial/java/generics/)