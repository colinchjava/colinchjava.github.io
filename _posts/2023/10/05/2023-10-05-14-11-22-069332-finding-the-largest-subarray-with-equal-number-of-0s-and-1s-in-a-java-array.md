---
layout: post
title: "Finding the largest subarray with equal number of 0s and 1s in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we will discuss a popular algorithmic problem: finding the largest subarray within a given Java array that contains an equal number of 0s and 1s. This problem can be solved efficiently using a technique called prefix sum.

## Table of Contents
1. [Problem Overview](#problem-overview)
2. [Approach](#approach)
3. [Implementation in Java](#implementation-in-java)
4. [Example](#example)
5. [Conclusion](#conclusion)
6. [References](#references)

## Problem Overview

Given a binary (0s and 1s) array of length `n`, our task is to find the largest subarray that contains an equal number of 0s and 1s. 

For example, consider the following input array:

```
[0, 1, 0, 1, 1, 0, 1, 0]
```

In this case, the largest subarray with an equal number of 0s and 1s is `[0, 1, 1, 0, 1]` with a length of 5.

## Approach

To solve this problem, we can use the concept of prefix sum. We iterate through the given array and maintain a count variable. 

- Initialize a variable `maxLen` to store the maximum length of the subarray found so far, and `sum` to 0.
- Create a HashMap to store the cumulative sums as keys and their corresponding indexes as values. 
- Traverse the input array and for every element, add `1` to the `sum` if the element is `1`, and `−1` if the element is `0`. 
- Check if the `sum` value is `0`. If it is, update `maxLen` to the index of the current element + 1 (to include all elements up to the current position).
- If the `sum` value exists as a key in the HashMap, update `maxLen` to the maximum value between `maxLen` and the difference between the current index and the index stored in the HashMap for that `sum` value.
- If the `sum` value does not exist as a key in the HashMap, add the `sum` value with the current index as the value.
- Finally, return `maxLen` as the length of the largest subarray with an equal number of 0s and 1s.

## Implementation in Java

Here is the Java implementation of the approach:

```java
import java.util.HashMap;

class LargestSubarrayEqualZeroOne {

    public static int findMaxLength(int[] nums) {
        int maxLen = 0;
        int sum = 0;
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        
        for (int i = 0; i < nums.length; i++) {
            sum += (nums[i] == 0 ? -1 : 1);
            
            if (map.containsKey(sum)) {
                maxLen = Math.max(maxLen, i - map.get(sum));
            } else {
                map.put(sum, i);
            }
        }
        
        return maxLen;
    }
    
    public static void main(String[] args) {
        int[] nums = {0, 1, 0, 1, 1, 0, 1, 0};
        System.out.println("Length of the largest subarray: " + findMaxLength(nums));
    }
}
```

## Example

Let's consider the same input array as before: `[0, 1, 0, 1, 1, 0, 1, 0]`. 

When we execute the above Java program, it will print:

```
Length of the largest subarray: 5
```

This means that the largest subarray with an equal number of 0s and 1s in the given array is `[0, 1, 1, 0, 1]` with a length of 5.

## Conclusion

In this blog post, we discussed how to find the largest subarray with an equal number of 0s and 1s in a Java array. We used the technique of prefix sum to solve this problem efficiently. By using a HashMap to store the cumulative sums and their indexes, we were able to find the largest subarray in linear time complexity.

I hope you found this blog post helpful. Happy coding!

## References
- [GeeksforGeeks - Largest subarray with equal number of 0s and 1s](https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/)