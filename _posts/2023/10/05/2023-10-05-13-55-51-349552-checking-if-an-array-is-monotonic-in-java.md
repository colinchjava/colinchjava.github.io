---
layout: post
title: "Checking if an array is monotonic in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

To determine if an array is monotonic, you can write a simple Java method that compares adjacent elements and checks if they are in the desired order. Here's an example code snippet that demonstrates how to check for monotonicity in an array:

```java
public class MonotonicArrayChecker {

    public static boolean isMonotonic(int[] arr) {
        boolean increasing = true;
        boolean decreasing = true;

        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < arr[i - 1]) {
                increasing = false;
            }

            if (arr[i] > arr[i - 1]) {
                decreasing = false;
            }
        }

        return increasing || decreasing;
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5}; // Monotonically increasing
        int[] arr2 = {5, 4, 3, 2, 1}; // Monotonically decreasing
        int[] arr3 = {1, 2, 2, 3, 4}; // Non-monotonic

        System.out.println(isMonotonic(arr1)); // Output: true
        System.out.println(isMonotonic(arr2)); // Output: true
        System.out.println(isMonotonic(arr3)); // Output: false
    }
}
```

In this code, the `isMonotonic` method takes an integer array `arr` as input and checks if it is monotonic. It uses two boolean variables, `increasing` and `decreasing`, to keep track of whether the array is monotonically increasing or decreasing. The loop iterates through the array, comparing each element with its previous element. If any element violates the desired order, the corresponding boolean variable is set to `false`.

Finally, the method returns `true` if either `increasing` or `decreasing` is `true`, indicating that the array is monotonic. Otherwise, it returns `false`.

In the `main` method, we test the `isMonotonic` method with different arrays and print the results. The output of the code shows whether each input array is monotonic or not.

Remember, this is just one way to check monotonicity in an array. Depending on the requirements of your specific use case, you may need to modify or optimize the code accordingly.

#java #monotonic-array