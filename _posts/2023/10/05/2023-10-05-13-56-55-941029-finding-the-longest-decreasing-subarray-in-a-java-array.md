---
layout: post
title: "Finding the longest decreasing subarray in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we'll discuss a common problem in array manipulation - finding the longest decreasing subarray in a Java array. We'll walk through the step-by-step process of identifying and implementing a solution for this problem. So let's get started!

## Table of Contents
- [Introduction](#introduction)
- [Approach](#approach)
- [Implementation](#implementation)
- [Conclusion](#conclusion)

## Introduction
Given an array of integers, we need to find the longest subarray within the array that is strictly decreasing. The subarray length refers to the number of elements in the subarray.

For example, if we have the array `[10, 5, 8, 3, 1, 6, 9, 2]`, the longest decreasing subarray is `[10, 5, 3, 1]`.

## Approach
To solve this problem, we can utilize a simple algorithm. We iterate through the array, keeping track of the current decreasing subarray's length and the maximum length. Whenever we encounter an element that is not strictly decreasing, we update the current length and check if it's greater than the maximum length. If it is, we update the maximum length.

## Implementation
Let's implement the algorithm in Java:

```java
public class LongestDecreasingSubarray {
    public static int findLongestDecreasingSubarray(int[] arr) {
        int maxLen = 0;
        int currentLen = 1;
        
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] < arr[i - 1]) {
                currentLen++;
            } else {
                maxLen = Math.max(maxLen, currentLen);
                currentLen = 1;
            }
        }
        
        return Math.max(maxLen, currentLen);
    }
    
    public static void main(String[] args) {
        int[] arr = {10, 5, 8, 3, 1, 6, 9, 2};
        int longestDecreasingSubarrayLength = findLongestDecreasingSubarray(arr);
        System.out.println("Longest Decreasing Subarray Length: " + longestDecreasingSubarrayLength);
    }
}
```

In the `findLongestDecreasingSubarray` method, we initialize `maxLen` and `currentLen` variables to zero and one, respectively. We iterate through the array, comparing each element with the previous one. If the current element is less than the previous one, we increment `currentLen`. Otherwise, we update `maxLen` with the maximum value between `maxLen` and `currentLen`, reset `currentLen` to one, and continue.

In the `main` method, we create a sample array, `arr`, and call the `findLongestDecreasingSubarray` method to find the length of the longest decreasing subarray. Finally, we print the result.

## Conclusion
Finding the longest decreasing subarray in a Java array is a common problem in array manipulation. With the algorithm and implementation provided in this blog post, you can easily solve this problem in Java. Feel free to try different arrays and test the implementation.

If you have any questions or suggestions, please leave a comment below. Happy programming!

#hashtags: #Java #arrays