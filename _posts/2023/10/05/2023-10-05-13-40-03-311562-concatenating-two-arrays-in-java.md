---
layout: post
title: "Concatenating two arrays in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

### 1. Using `System.arraycopy()`
The `System.arraycopy()` method is a low-level method that performs a native copy of the elements from one array to another. Here's how you can use it to concatenate two arrays:

```java
int[] array1 = {1, 2, 3};
int[] array2 = {4, 5, 6};

int[] result = new int[array1.length + array2.length];
System.arraycopy(array1, 0, result, 0, array1.length);
System.arraycopy(array2, 0, result, array1.length, array2.length);
```

In the above example, we create a new array `result` with a length equal to the sum of the lengths of `array1` and `array2`. Then we use `System.arraycopy()` twice to copy the elements from `array1` and `array2` into the `result` array.

### 2. Using `Arrays.copyOf()`
The `Arrays.copyOf()` method is a convenience method that simplifies the process of copying arrays. Here's how you can use it to concatenate two arrays:

```java
int[] array1 = {1, 2, 3};
int[] array2 = {4, 5, 6};

int[] result = Arrays.copyOf(array1, array1.length + array2.length);
System.arraycopy(array2, 0, result, array1.length, array2.length);
```

In this example, we use `Arrays.copyOf()` to create a new array `result` with a length equal to the sum of the lengths of `array1` and `array2`, and copy the elements of `array1` into `result`. Then we use `System.arraycopy()` to copy the elements of `array2` into `result`, starting from the index where `array1` ends.

### Summary
Both `System.arraycopy()` and `Arrays.copyOf()` provide ways to concatenate two arrays in Java. While `System.arraycopy()` is a low-level method, `Arrays.copyOf()` is a more convenient method that simplifies the process. You can choose the method that suits your specific needs and coding style.

[#java]