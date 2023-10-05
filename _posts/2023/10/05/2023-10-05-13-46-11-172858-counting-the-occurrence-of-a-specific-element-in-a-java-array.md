---
layout: post
title: "Counting the occurrence of a specific element in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with arrays in Java, it is often necessary to determine the number of occurrences of a specific element within the array. In this article, we will explore different approaches to accomplish this task efficiently.

## Method 1: Linear Search

A simple and straightforward way to count the occurrence of an element in a Java array is by performing a linear search. Here's an example code snippet that demonstrates this method:

```java
public static int countOccurrences(int[] array, int element) {
    int count = 0;
    for (int num : array) {
        if (num == element) {
            count++;
        }
    }
    return count;
}
```

In this method, we iterate over each element of the array and increment the count whenever the element matches the given element. Finally, we return the count as the result.

While this approach works fine for small arrays, it has a time complexity of O(n), where n is the size of the array. Hence, for large arrays, it might not be the most optimal solution.

## Method 2: Using Stream API

Java 8 introduced the Stream API, which provides a more concise way to perform operations on collections, including arrays. We can leverage the Stream API to count the occurrences of an element in an array. Here's an example:

```java
import java.util.Arrays;

public static long countOccurrences(int[] array, int element) {
    return Arrays.stream(array).filter(num -> num == element).count();
}
```

In this method, we convert the array into a stream, filter out the elements that do not match the given element, and then count the remaining elements using the `count()` method. The result is returned as a `long` value.

Using the Stream API simplifies the code and makes it more expressive. However, it may have a slightly higher overhead compared to the linear search method.

## Conclusion

Counting the occurrence of a specific element in a Java array can be achieved using either a linear search approach or by leveraging the Stream API introduced in Java 8. The choice of method depends on the size of the array and the performance requirements of the application.

Remember to choose the most appropriate method based on the specific needs of your application to achieve optimal performance.