---
layout: post
title: "Finding the longest increasing subarray in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we will explore how to find the longest increasing subarray in a Java array efficiently. A subarray is a contiguous part of an array, and an increasing subarray is one where the elements are arranged in ascending order.

## Introduction
Given an array, we need to find the longest subarray where the elements are in increasing order. For example, given the array [1, 3, 2, 4, 5, 7, 6, 8], the longest increasing subarray is [2, 4, 5, 7].

## Algorithm
To solve this problem, we can use a two-pointer approach. We will iterate through the array with two pointers, `start` and `end`, representing the start and end indices of the current subarray.

We will initialize both pointers to 0, and as we iterate through the array, we will check if the next element is greater than the current element. If it is, we move the `end` pointer to the right. If not, we calculate the length of the current subarray and update the `start` pointer to the next element.

At each iteration, we also keep track of the maximum length of the increasing subarray found so far. This way, we can easily identify the longest increasing subarray when we finish iterating through the array.

Here is the Java code that implements this algorithm:

```java
public class LongestIncreasingSubarray {
    public static void findLongestIncreasingSubarray(int[] arr) {
        int n = arr.length;
        int start = 0, end = 0;
        int maxLength = 1; // minimum length of an increasing subarray is 1

        while (end < n - 1) {
            if (arr[end + 1] > arr[end]) {
                end++;
            } else {
                int length = end - start + 1;
                if (length > maxLength) {
                    maxLength = length;
                }
                start = end + 1;
                end = start;
            }
        }

        int length = end - start + 1;
        if (length > maxLength) {
            maxLength = length;
        }

        System.out.println("Longest increasing subarray length: " + maxLength);
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 2, 4, 5, 7, 6, 8};
        findLongestIncreasingSubarray(arr);
    }
}
```

## Complexity Analysis
The time complexity of this algorithm is O(n), where n is the size of the input array. This is because we iterate through the array only once, comparing each element with the next one.

The space complexity is O(1) since we are using only a constant amount of extra space to store the pointers and variables.

## Conclusion
In this blog post, we discussed the problem of finding the longest increasing subarray in a Java array. We presented an efficient algorithm using a two-pointer approach and provided the Java implementation.

By using this algorithm, you can easily find the longest increasing subarray in an array and utilize it for further processing in your Java applications.

#Java #Algorithms