---
layout: post
title: "Checking if an array is sorted in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, you might come across situations where you need to check whether an array is sorted or not. There are several ways to accomplish this, ranging from simple to more complex algorithms. In this article, we will explore a straightforward approach to determine if an array is sorted in Java.

## The Approach

The basic idea is to iterate through the array and compare each element with its adjacent element. If, at any point, we find that an element is greater than its next element, we can conclude that the array is not sorted. On the other hand, if we successfully iterate through the entire array without finding any such pair, we can confirm that the array is sorted.

## Implementation

Let's take a look at the Java code to implement this algorithm:

```java
public class ArraySortChecker {
    
    public static boolean isSorted(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < arr[i-1]) {
                return false;
            }
        }
        return true;
    }
    
    public static void main(String[] args) {
        int[] sortedArr = {1, 2, 3, 4, 5};
        int[] unsortedArr = {5, 4, 3, 2, 1};
        
        System.out.println("Is the sortedArr sorted? " + isSorted(sortedArr));
        System.out.println("Is the unsortedArr sorted? " + isSorted(unsortedArr));
    }
}
```

In the `isSorted()` method, we iterate through the array starting from the second element (`i = 1`). We compare each element with its previous element (`arr[i-1]`). If we find that an element is smaller than its previous element, we return `false` to indicate that the array is not sorted. Otherwise, we continue the iteration. If we reach the end of the loop without finding any such pair, we return `true` to indicate that the array is sorted.

In the `main()` method, we create two arrays - `sortedArr` and `unsortedArr`. We call the `isSorted()` method to check if each array is sorted or not and display the result.

## Testing

When running the above code, you should see the following output:

```
Is the sortedArr sorted? true
Is the unsortedArr sorted? false
```

As expected, the `sortedArr` returns `true` since it is sorted in ascending order, while the `unsortedArr` returns `false` as it is not sorted.

## Conclusion

In this blog post, we explored a simple approach to check if an array is sorted in Java. By comparing each element with its preceding element, we can determine if the array is arranged in ascending order. This algorithm can be used in various situations where sorting is required, such as analyzing data or implementing binary search algorithms.