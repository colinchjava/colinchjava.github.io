---
layout: post
title: "Implementing a LRU cache using LinkedHashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with cache systems, it's often necessary to implement a Least Recently Used (LRU) cache to efficiently manage the storage of frequently accessed data. In Java, we can utilize the `LinkedHashMap` data structure to implement a LRU cache.

## What is a LRU Cache?

An LRU cache is a cache eviction policy that removes the least recently used items first when the cache reaches its maximum capacity. This policy ensures that the most recently used items stay in the cache, as they are likely to be accessed again in the near future.

## Using LinkedHashMap

In Java, `LinkedHashMap` extends `HashMap` and maintains the order of elements by the order of their insertion. This makes it a perfect candidate for implementing a LRU cache, as we can take advantage of the built-in ordering to easily remove the least recently used elements.

Here's an example implementation:

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LRUCache<K,V> extends LinkedHashMap<K,V> {
    private int capacity;

    public LRUCache(int capacity) {
        super(capacity, 0.75f, true);
        this.capacity = capacity;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K,V> eldest) {
        return size() > capacity;
    }
}
```

In this implementation, we extend `LinkedHashMap` and override the `removeEldestEntry` method. This method is called by the `put` method in `LinkedHashMap` before inserting a new entry. By returning `true` when the size exceeds the capacity, we ensure that the eldest (least recently used) entry is removed.

## Example Usage

```java
LRUCache<Integer, String> cache = new LRUCache<>(3);
cache.put(1, "One");
cache.put(2, "Two");
cache.put(3, "Three");
System.out.println(cache); // {1=One, 2=Two, 3=Three}

cache.get(1); // Access the value associated with key 1
System.out.println(cache); // {2=Two, 3=Three, 1=One}

cache.put(4, "Four"); // Adding a new entry, triggers eviction
System.out.println(cache); // {3=Three, 1=One, 4=Four}
```

In this example, we create a `LRUCache` with a capacity of 3. We put three entries into the cache and then access the value associated with key 1. As a result, the order is updated and the least recently used entry (key 2) is evicted when a new entry (key 4) is added.

## Conclusion

Using `LinkedHashMap` allows you to easily implement a LRU cache in Java. By overriding the `removeEldestEntry` method, you can customize the eviction behavior according to your specific needs. This implementation provides an efficient and easy-to-use LRU cache mechanism for managing frequently accessed data.

# References
- [LinkedHashMap javadoc](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/LinkedHashMap.html)