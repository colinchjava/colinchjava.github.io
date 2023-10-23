---
layout: post
title: "Iterating over a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, the `HashMap` class is a widely used data structure that allows you to store key-value pairs. Sometimes, you may need to iterate over the elements of a `HashMap` to perform certain operations. In this article, we will explore different ways to iterate over a `HashMap` in Java.

## Method 1: Using EntrySet

The `entrySet()` method in the `HashMap` class returns a set view of the key-value pairs contained in the map. We can use this set to iterate over the elements of the `HashMap`.

```java
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "Apple");
map.put(2, "Banana");
map.put(3, "Orange");

for (Map.Entry<Integer, String> entry : map.entrySet()) {
    int key = entry.getKey();
    String value = entry.getValue();
    System.out.println("Key: " + key + ", Value: " + value);
}
```

In the above code, we use a for-each loop to iterate over the `entrySet()` of the `HashMap`. We retrieve the key-value pair from each entry using the `getKey()` and `getValue()` methods, and then print them.

## Method 2: Using KeySet

The `keySet()` method in the `HashMap` class returns a set view of the keys contained in the map. We can use this set to iterate over the keys and retrieve their corresponding values from the `HashMap`.

```java
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "Apple");
map.put(2, "Banana");
map.put(3, "Orange");

for (Integer key : map.keySet()) {
    String value = map.get(key);
    System.out.println("Key: " + key + ", Value: " + value);
}
```

Here, we use a for-each loop to iterate over the `keySet()` of the `HashMap`. For each key, we use the `get()` method to retrieve the corresponding value from the `HashMap`.

## Conclusion

Iterating over a `HashMap` in Java is essential when you need to manipulate or perform operations on the key-value pairs. In this article, we have explored two common methods for iterating over a `HashMap` using `entrySet()` and `keySet()`.

Remember to choose the appropriate method depending on your specific use case.