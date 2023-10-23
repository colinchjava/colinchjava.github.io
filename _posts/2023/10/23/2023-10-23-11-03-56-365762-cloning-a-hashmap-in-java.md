---
layout: post
title: "Cloning a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

`HashMap` is a commonly used data structure in Java that stores key-value pairs. Sometimes, there is a need to create a copy or clone of an existing `HashMap` for various purposes. In this blog post, we will explore how to clone a `HashMap` in Java.

## Table of Contents

- [Introduction](#introduction)
- [Shallow Cloning](#shallow-cloning)
- [Deep Cloning](#deep-cloning)
- [Conclusion](#conclusion)

## Introduction

Cloning a `HashMap` means creating a new instance of `HashMap` with the same key-value pairs as the original `HashMap`. It is important to understand the difference between shallow cloning and deep cloning in this context.

## Shallow Cloning

Shallow cloning refers to creating a new `HashMap` instance where the keys and values still refer to the same objects as the original `HashMap`. In other words, changes made to the objects in either the original or cloned `HashMap` will reflect in both.

To perform shallow cloning, we can use the `clone()` method provided by the `HashMap` class. Here's an example:

```java
HashMap<Integer, String> originalHashMap = new HashMap<>();
originalHashMap.put(1, "one");
originalHashMap.put(2, "two");

HashMap<Integer, String> clonedHashMap = (HashMap<Integer, String>) originalHashMap.clone();

clonedHashMap.put(3, "three");

System.out.println(originalHashMap); // Output: {1=one, 2=two, 3=three}
System.out.println(clonedHashMap); // Output: {1=one, 2=two, 3=three}
```

As you can see, modifying the cloned `HashMap` also affects the original `HashMap`. This is because the keys and values are still referencing the same objects.

## Deep Cloning

Deep cloning, on the other hand, involves creating a new `HashMap` instance where the keys and values refer to separate copies of the original objects. Changes made to the objects in either the original or cloned `HashMap` will not affect each other.

To achieve deep cloning, we need to manually iterate over the original `HashMap` and create new instances of the objects within the cloned `HashMap`. Here's an example:

```java
HashMap<Integer, String> originalHashMap = new HashMap<>();
originalHashMap.put(1, "one");
originalHashMap.put(2, "two");

HashMap<Integer, String> clonedHashMap = new HashMap<>();
for (Map.Entry<Integer, String> entry : originalHashMap.entrySet()) {
    clonedHashMap.put(entry.getKey(), new String(entry.getValue()));
}

clonedHashMap.put(3, "three");

System.out.println(originalHashMap); // Output: {1=one, 2=two}
System.out.println(clonedHashMap); // Output: {1=one, 2=two, 3=three}
```

In the above example, we create new `String` objects for the values while iterating over the original `HashMap`. This ensures that changes made to the values in one `HashMap` do not affect the other.

## Conclusion

Cloning a `HashMap` in Java allows us to create a duplicate of an existing `HashMap`. Depending on the scenario, we can choose between shallow cloning, where the keys and values reference the same objects, or deep cloning, where the keys and values refer to separate copies of the original objects.