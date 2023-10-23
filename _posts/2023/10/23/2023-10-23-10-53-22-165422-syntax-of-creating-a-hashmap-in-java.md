---
layout: post
title: "Syntax of creating a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, a `HashMap` is a commonly used data structure that stores key-value pairs. It allows for efficient retrieval and insertion of elements, making it ideal for many applications. Here is the syntax for creating a `HashMap` in Java:

```java
// Import the HashMap class
import java.util.HashMap;

// Create a new HashMap object
HashMap<KeyType, ValueType> hashMapName = new HashMap<>();
```

Let's break down the above syntax:

- First, we import the `HashMap` class from the `java.util` package.
- Next, we declare and initialize a new `HashMap` object named `hashMapName`.
- Inside the angle brackets (`<>`), you need to specify the types of the key and value that the `HashMap` will hold. Replace `KeyType` with the type of your key and `ValueType` with the type of your value.

For example, if you want to create a `HashMap` with keys of type `String` and values of type `Integer`, you would use the following syntax:

```java
HashMap<String, Integer> hashMapName = new HashMap<>();
```

You can then add key-value pairs to the `HashMap` using the `put()` method:

```java
hashMapName.put("key1", 123);
hashMapName.put("key2", 456);
```

To access the value associated with a specific key, you can use the `get()` method:

```java
Integer value = hashMapName.get("key1");
```

The `HashMap` class in Java provides various other methods for manipulating and iterating over the elements it contains. You can refer to the [official Java documentation for HashMap](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html) for more details.

Remember to import the `java.util.HashMap` class at the start of your Java file to use `HashMap` in your code.

---

Hashtags: #Java #HashMap