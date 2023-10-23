---
layout: post
title: "Creating a synchronized HashMap in Java"
description: " "
date: 2023-10-23
tags: [synchronized]
comments: true
share: true
---

In Java, the `HashMap` class provided in the `java.util` package is a widely-used data structure for storing key-value pairs. However, it is not inherently thread-safe, meaning it may encounter issues when accessed concurrently by multiple threads. To ensure thread safety, we can use the `Collections.synchronizedMap` method to create a synchronized version of the `HashMap`.

Here's how you can create a synchronized `HashMap` in Java:

```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class SynchronizedHashMapExample {

    public static void main(String[] args) {
        // Create a synchronized HashMap
        Map<String, Integer> synchronizedMap = Collections.synchronizedMap(new HashMap<>());

        // Add elements to the synchronized map
        synchronizedMap.put("apple", 1);
        synchronizedMap.put("banana", 2);
        synchronizedMap.put("orange", 3);

        // Perform operations on the synchronized map
        synchronized (synchronizedMap) {
            // Access and modify the synchronized map
            for (String key : synchronizedMap.keySet()) {
                System.out.println(key + ": " + synchronizedMap.get(key));
            }
        }
    }
}
```

In the above example, we utilize the `Collections.synchronizedMap` method to create a synchronized version of the `HashMap`. This method returns a synchronized wrapper of the given map, ensuring that all operations on the map are thread-safe.

To perform operations on the synchronized map, we enclose the critical section of code within a `synchronized` block. This guarantees that only one thread can access the map at a time, preventing concurrent modifications.

Keep in mind that while the synchronized map ensures thread safety for individual operations, it does not provide atomicity for compound actions that require multiple operations. In such cases, you may need to use other synchronization mechanisms like locks or concurrent classes.

By using a synchronized `HashMap`, you can safely and effectively handle concurrent access to shared data in multi-threaded applications.

**References:**

- [HashMap JavaDoc](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html)
- [Collections JavaDoc](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Collections.html)

#java #synchronized