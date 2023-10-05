---
layout: post
title: "Finding the smallest k elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this tutorial, we will discuss how to find the smallest K elements in a Java array. This can be a common scenario in programming where you need to find the smallest values in an array for further processing or analysis.

## Table of Contents
1. [Approach 1: Sorting the Array](#approach-1-sorting-the-array)
2. [Approach 2: Using a Priority Queue](#approach-2-using-a-priority-queue)

## Approach 1: Sorting the Array
One straightforward approach to find the smallest K elements in a Java array is by sorting the array in ascending order and then selecting the first K elements.

Here's an example code snippet that demonstrates this approach:

```java
import java.util.Arrays;

public class SmallestKElements {
    public static int[] findSmallestKElements(int[] array, int k) {
        Arrays.sort(array);
        int[] result = new int[k];
        System.arraycopy(array, 0, result, 0, k);
        return result;
    }

    public static void main(String[] args) {
        int[] array = {8, 2, 6, 9, 1, 4, 3, 7, 5};
        int k = 3;
        int[] smallestKElements = findSmallestKElements(array, k);
        System.out.println("Smallest " + k + " elements: " + Arrays.toString(smallestKElements));
    }
}
```

In this code, we first sort the array using `Arrays.sort()` method. Then, we create a new array `result` of size `k`, and using `System.arraycopy()`, we copy the first `k` elements from the sorted array to the `result` array. Finally, we return the `result` array containing the smallest `k` elements.

## Approach 2: Using a Priority Queue
An alternative approach is to use a Priority Queue, also known as a Min Heap, to find the smallest K elements without sorting the entire array.

Here's an example code snippet that demonstrates this approach:

```java
import java.util.PriorityQueue;

public class SmallestKElements {
    public static int[] findSmallestKElements(int[] array, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num : array) {
            pq.offer(num);
        }

        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = pq.poll();
        }

        return result;
    }

    public static void main(String[] args) {
        int[] array = {8, 2, 6, 9, 1, 4, 3, 7, 5};
        int k = 3;
        int[] smallestKElements = findSmallestKElements(array, k);
        System.out.println("Smallest " + k + " elements: " + Arrays.toString(smallestKElements));
    }
}
```

In this code, we use a `PriorityQueue` to store the elements from the array. The `PriorityQueue` automatically keeps the elements in ascending order based on their values. We iterate over the array and insert each element into the `PriorityQueue` using the `offer()` method.

Then, we create a new array `result` of size `k` and repeatedly call `poll()` on the `PriorityQueue` `k` times to extract the smallest elements. Finally, we return the `result` array containing the smallest `k` elements.

## Conclusion
By using either the sorting or Priority Queue approach, you can easily find the smallest K elements in a Java array. Choose the approach that best suits your needs based on the size of the array and the specific requirements of your program.

I hope you found this tutorial helpful! If you have any questions or suggestions, feel free to leave a comment below.

#programming #java