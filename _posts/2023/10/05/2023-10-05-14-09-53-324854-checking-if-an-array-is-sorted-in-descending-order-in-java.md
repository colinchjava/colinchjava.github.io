---
layout: post
title: "Checking if an array is sorted in descending order in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Here's an example code snippet that demonstrates how to check if an array is sorted in descending order in Java:

```java
public class Main {
    public static boolean isSortedDescending(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > arr[i - 1]) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        int[] arr1 = {5, 4, 3, 2, 1};
        int[] arr2 = {1, 2, 3, 4, 5};

        System.out.println("arr1 is sorted in descending order: " + isSortedDescending(arr1));
        System.out.println("arr2 is sorted in descending order: " + isSortedDescending(arr2));
    }
}
```

Output:
```
arr1 is sorted in descending order: true
arr2 is sorted in descending order: false
```

In the code above, the `isSortedDescending` method checks each element in the array starting from the second element (`arr[i]`) and compares it with the previous element (`arr[i - 1]`). If `arr[i]` is greater than `arr[i - 1]`, it means the array is not sorted in descending order, so the method returns `false`. If the loop completes without finding any out-of-order elements, the method returns `true`, indicating that the array is sorted in descending order.

You can use this code snippet to check if any given array is sorted in descending order in your Java programs.