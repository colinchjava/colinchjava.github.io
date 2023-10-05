---
layout: post
title: "Merging multiple arrays into one array in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, there are various ways to merge multiple arrays into one array efficiently. In this blog post, we will explore two common approaches to achieve this: the manual approach using loops and the built-in `System.arraycopy()` method.

## Table of Contents
- [Manual Approach](#manual-approach)
- [`System.arraycopy()` Method](#system-arraycopy-method)
- [Conclusion](#conclusion)

## Manual Approach

The manual approach involves using loops to iterate through each array and copy its elements into a new resulting array.

Here's an example code snippet that demonstrates this approach:

```java
public class ArrayMerger {
    public static int[] mergeArrays(int[]... arrays) {
        int totalLength = 0;
        for (int[] arr : arrays) {
            totalLength += arr.length;
        }

        int[] mergedArray = new int[totalLength];
        int index = 0;
        for (int[] arr : arrays) {
            for (int element : arr) {
                mergedArray[index++] = element;
            }
        }

        return mergedArray;
    }

    public static void main(String[] args) {
        int[] array1 = {1, 2, 3};
        int[] array2 = {4, 5};
        int[] array3 = {6, 7, 8, 9};

        int[] merged = mergeArrays(array1, array2, array3);
        System.out.println(Arrays.toString(merged));
    }
}
```

In this example, the `mergeArrays()` method takes in multiple arrays as varargs. It first calculates the total length of the merged array, initializes a new array with this length, and then iterates through each array, copying its elements into the merged array.

The output of the above code will be:
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## `System.arraycopy()` Method

The `System.arraycopy()` method is a built-in Java method that allows for efficient copying of arrays. It eliminates the need for manual iteration through each array and copying elements.

Here's an example code snippet that demonstrates using the `System.arraycopy()` method to merge arrays:

```java
public class ArrayMerger {
    public static int[] mergeArrays(int[]... arrays) {
        int totalLength = 0;
        for (int[] arr : arrays) {
            totalLength += arr.length;
        }

        int[] mergedArray = new int[totalLength];
        int index = 0;
        for (int[] arr : arrays) {
            System.arraycopy(arr, 0, mergedArray, index, arr.length);
            index += arr.length;
        }

        return mergedArray;
    }

    public static void main(String[] args) {
        int[] array1 = {1, 2, 3};
        int[] array2 = {4, 5};
        int[] array3 = {6, 7, 8, 9};

        int[] merged = mergeArrays(array1, array2, array3);
        System.out.println(Arrays.toString(merged));
    }
}
```

In this example, the `System.arraycopy()` method is used to copy each array into the merged array. The `System.arraycopy()` method takes in the source array, starting position in the source array, destination array, starting position in the destination array, and the length to copy.

The output of the above code will be the same as the previous example.

## Conclusion

Merging multiple arrays into one array can be accomplished using a manual approach using loops or the built-in `System.arraycopy()` method. Both approaches are efficient and provide flexibility depending on your specific use case.

By using the `mergeArrays()` method provided in this blog post, you can merge any number of arrays into a single array effortlessly in Java.

\#java #array-merging