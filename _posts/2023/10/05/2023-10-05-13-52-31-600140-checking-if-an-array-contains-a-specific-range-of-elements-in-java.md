---
layout: post
title: "Checking if an array contains a specific range of elements in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

### Approach 1: Loop through the Array

One approach is to loop through the array and check if each element falls within the desired range. Here is an example code snippet that demonstrates this approach:

```java
public static boolean arrayContainsRange(int[] arr, int start, int end) {
    for (int i : arr) {
        if (i < start || i > end) {
            return false;
        }
    }
    return true;
}
```

In this code snippet, we define a method `arrayContainsRange` that takes an array `arr`, a start index `start`, and an end index `end`. It loops through each element in the array and checks if it is less than the start or greater than the end. If any element falls outside the desired range, it returns `false`. If all elements fall within the range, it returns `true`.

### Approach 2: Using Stream API

Another approach is to use Java 8's Stream API to perform the range check. Here is an example code snippet that demonstrates this approach:

```java
import java.util.Arrays;

public static boolean arrayContainsRange(int[] arr, int start, int end) {
    return Arrays.stream(arr).allMatch(i -> i >= start && i <= end);
}
```

In this code snippet, we use the `Arrays.stream` method to convert the array into a stream of integers. Then, we use the `allMatch` method to check if all elements in the stream satisfy the given condition (i.e., `i >= start && i <= end`). If all elements pass the condition, it returns `true`; otherwise, it returns `false`.

### Conclusion

In this blog post, we explored two different approaches to check if an array contains a specific range of elements in Java. Depending on your preference and the requirements of your application, you can choose the approach that best suits your needs.

Remember that these are just two of the many possible approaches to solve this problem. Consider the size of the array, the range of elements to check, and the performance implications when selecting the most appropriate approach.

#programming #java