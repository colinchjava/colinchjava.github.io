---
layout: post
title: "Rotating elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, you might often encounter situations where you need to rotate the elements of an array. Array rotation refers to shifting the position of elements within an array in a circular manner. For example, if you rotate an array `[1, 2, 3, 4, 5]` by two positions to the right, it becomes `[4, 5, 1, 2, 3]`.

In this tutorial, we will explore three different methods to rotate elements in a Java array. We will cover the following approaches:

1. Using an additional array
2. Using a temporary variable
3. Using array reversal

## Using an Additional Array

The simplest approach to rotate elements in an array is to create a new array and copy the elements in their new positions. Here is a Java code snippet that demonstrates this method:

```java
public static void rotateArray(int[] arr, int numberOfRotations) {
    int[] tempArr = new int[arr.length];

    for (int i = 0; i < arr.length; i++) {
        int newPosition = (i + numberOfRotations) % arr.length;
        tempArr[newPosition] = arr[i];
    }

    for (int i = 0; i < arr.length; i++) {
        arr[i] = tempArr[i];
    }
}
```

To use this method, you need to pass the array `arr` and the number of rotations `numberOfRotations` as parameters to the `rotateArray` method.

## Using a Temporary Variable

Another approach to rotate the elements of an array is by using a temporary variable to store the last element and then shifting all the other elements. Here is a simple Java code snippet that demonstrates this method:

```java
public static void rotateArray(int[] arr, int numberOfRotations) {
    for (int i = 0; i < numberOfRotations; i++) {
        int temp = arr[arr.length - 1];

        for (int j = arr.length - 1; j > 0; j--) {
            arr[j] = arr[j - 1];
        }

        arr[0] = temp;
    }
}
```

This `rotateArray` method takes the array `arr` and the number of rotations `numberOfRotations` as parameters.

## Using Array Reversal

The third method involves reversing the array elements in two steps. First, we reverse the entire array. Then, we reverse the subarrays before and after the rotation point. This effectively rotates the array elements. Here is a Java code snippet that demonstrates this method:

```java
public static void rotateArray(int[] arr, int numberOfRotations) {
    reverseArray(arr, 0, arr.length - 1);
    reverseArray(arr, 0, numberOfRotations - 1);
    reverseArray(arr, numberOfRotations, arr.length - 1);
}

private static void reverseArray(int[] arr, int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;

        start++;
        end--;
    }
}
```

To use this method, you need to pass the array `arr` and the number of rotations `numberOfRotations` as parameters to the `rotateArray` method.

## Conclusion

In this tutorial, we covered three different methods to rotate elements in a Java array. You can choose the method that best suits your requirements and implement it in your own projects. Remember to consider factors such as performance and space complexity when making your choice.

Feel free to experiment with the code snippets provided and explore other ways to rotate elements in Java arrays. Enjoy coding!

**#java #arrays**