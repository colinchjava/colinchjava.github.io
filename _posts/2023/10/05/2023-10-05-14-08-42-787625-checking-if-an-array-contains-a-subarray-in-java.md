---
layout: post
title: "Checking if an array contains a subarray in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Sometimes, while working with arrays in Java, we need to determine whether one array is a subarray of another. This can be useful in various scenarios, such as checking if a given pattern exists in a larger array or comparing subsequences. In this blog post, we will explore different approaches to solve this problem.

### Approach 1: Using nested loops

The most straightforward way to check if an array contains a subarray is by using nested loops. We iterate over each element of the main array and, for each element, iterate over the subarray. If all elements of the subarray are found consecutively in the main array, we conclude that the main array contains the subarray.

```java
public static boolean containsSubarray(int[] mainArray, int[] subArray) {
    int mainLen = mainArray.length;
    int subLen = subArray.length;

    for (int i = 0; i <= mainLen - subLen; i++) {
        int j;
        for (j = 0; j < subLen; j++) {
            if (mainArray[i + j] != subArray[j]) {
                break;
            }
        }
        if (j == subLen) {
            return true;
        }
    }
    return false;
}
```
This approach has a time complexity of O(n * m), where n is the length of the main array and m is the length of the subarray.

### Approach 2: Using the indexOf method

In Java, arrays are objects, and the `Arrays` class provides several utility methods to perform operations on arrays. One such method is `indexOf`, which can be used to find the index of a specific value in an array.

```java
import java.util.Arrays;

public static boolean containsSubarray(int[] mainArray, int[] subArray) {
    String mainStr = Arrays.toString(mainArray);
    String subStr = Arrays.toString(subArray);

    return mainStr.indexOf(subStr) != -1;
}
```

In this approach, we convert both the main array and subarray to `String` objects using the `Arrays.toString` method. We then use the `indexOf` method to check if the subarray exists in the main array.

### Approach 3: Using the Apache Commons Lang library

If you are using the Apache Commons Lang library in your Java project, you can leverage the `ArrayUtils` class to check if an array contains a subarray.

```java
import org.apache.commons.lang3.ArrayUtils;

public static boolean containsSubarray(int[] mainArray, int[] subArray) {
    return ArrayUtils.indexOf(mainArray, subArray) != -1;
}
```

In this approach, we use the `ArrayUtils.indexOf` method, which searches the main array for the subarray and returns the index if found. If the subarray is not present, the method returns -1.

Both approach 2 and approach 3 have a time complexity of O(n), where n is the length of the main array.

To use the Apache Commons Lang library, you can add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.12.0</version>
</dependency>
```

In conclusion, we have explored multiple approaches to checking if an array contains a subarray in Java. Depending on your requirements and project setup, you can choose the approach that best suits your needs.

#java #arrays