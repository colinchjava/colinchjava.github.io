---
layout: post
title: "Updating elements in a HashMap in Java"
description: " "
date: 2023-10-23
tags: [HashMap]
comments: true
share: true
---

In Java, the `HashMap` class is commonly used to store key-value pairs. Sometimes, we need to update the value associated with a particular key in a `HashMap`. In this blog post, we will explore different methods to update elements in a `HashMap` in Java.

## Table of Contents
- [Method 1: Using the `put()` method](#method-1-using-the-put-method)
- [Method 2: Using the `replace()` method](#method-2-using-the-replace-method)
- [Method 3: Using the `compute()` method](#method-3-using-the-compute-method)

## Method 1: Using the `put()` method

One way to update a value in a `HashMap` is to use the `put()` method. This method replaces the existing value associated with the specified key or adds a new key-value pair if the key does not already exist.

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 5); // Adding a new key-value pair

// Updating the value associated with the key "apple"
map.put("apple", 10); 

System.out.println(map); // Output: {apple=10}
```

In the above example, we first add a key-value pair to the `HashMap` using the `put()` method. Then, we update the value associated with the key "apple" to 10 using the `put()` method again. Finally, we print the `HashMap` to verify the value has been updated.

## Method 2: Using the `replace()` method

Another approach to update an element in a `HashMap` is to use the `replace()` method. This method replaces the value associated with the specified key only if it is already present in the `HashMap`.

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("banana", 8);

// Updating the value associated with the key "banana"
map.replace("banana", 12);

System.out.println(map); // Output: {banana=12}
```

In the above example, we first add a key-value pair to the `HashMap` using the `put()` method. Then, we update the value associated with the key "banana" to 12 using the `replace()` method. Finally, we print the `HashMap` to verify the value has been updated.

## Method 3: Using the `compute()` method

The `compute()` method provides a powerful way to update elements in a `HashMap` by applying a function to the existing and new values.

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("orange", 15);

// Updating the value associated with the key "orange" by incrementing it by 5
map.compute("orange", (key, value) -> value + 5);

System.out.println(map); // Output: {orange=20}
```

In the above example, we first add a key-value pair to the `HashMap` using the `put()` method. Then, we update the value associated with the key "orange" by incrementing it by 5 using the `compute()` method. Finally, we print the `HashMap` to verify the value has been updated.

## Conclusion

In this blog post, we explored different methods to update elements in a `HashMap` in Java. The `put()`, `replace()`, and `compute()` methods provide different ways to update values in a `HashMap` based on specific requirements. By utilizing these methods effectively, you can easily modify the elements in a `HashMap` to reflect the desired changes.

**References:**
- [Oracle Documentation: HashMap](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/HashMap.html)

**#java #HashMap**