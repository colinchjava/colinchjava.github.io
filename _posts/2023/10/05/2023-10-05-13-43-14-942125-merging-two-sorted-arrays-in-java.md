---
layout: post
title: "Merging two sorted arrays in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we will explore how to merge two sorted arrays in Java. Merging two sorted arrays is a common operation when dealing with algorithms and data structures. It involves combining two arrays into one while maintaining the sorted order.

## Table of Contents
- [Approach 1: Using Extra Space](#approach-1-using-extra-space)
- [Approach 2: In-Place Merge](#approach-2-in-place-merge)
- [Conclusion](#conclusion)

## Approach 1: Using Extra Space

The first approach to merge two sorted arrays involves creating a new array to store the merged result. The steps are as follows:

1. Create a new array with a size equal to the sum of the lengths of the input arrays.
2. Initialize three pointers: `i`, `j`, and `k`. Pointer `i` represents the current element of the first array, pointer `j` represents the current element of the second array, and pointer `k` represents the current position in the merged array.
3. Iterate through both arrays until either `i` reaches the end of the first array or `j` reaches the end of the second array.
4. Compare the elements at the current positions `i` and `j`. If the element in the first array is smaller or equal, add it to the merged array and increment `i`. Otherwise, add the element from the second array and increment `j`.
5. After reaching the end of either array, append the remaining elements from the other array to the merged array.
6. Finally, return the merged array.

Here's the Java implementation of the above approach:

```java
public class MergeSortedArrays {
    public static int[] mergeArrays(int[] arr1, int[] arr2) {
        int[] mergedArray = new int[arr1.length + arr2.length];
        int i = 0, j = 0, k = 0;
        
        while (i < arr1.length && j < arr2.length) {
            if (arr1[i] <= arr2[j]) {
                mergedArray[k++] = arr1[i++];
            } else {
                mergedArray[k++] = arr2[j++];
            }
        }
        
        while (i < arr1.length) {
            mergedArray[k++] = arr1[i++];
        }
        
        while (j < arr2.length) {
            mergedArray[k++] = arr2[j++];
        }
        
        return mergedArray;
    }
}
```

## Approach 2: In-Place Merge

The second approach to merge two sorted arrays is to perform an in-place merge, i.e., merging the arrays without using extra space. This approach optimizes the space complexity by merging the arrays directly without the need for a separate merged array.

Here's the Java implementation of the in-place merge:

```java
public class MergeSortedArrays {
    public static void mergeInPlace(int[] arr1, int[] arr2, int m, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;
        
        while (i >= 0 && j >= 0) {
            if (arr1[i] > arr2[j]) {
                arr1[k--] = arr1[i--];
            } else {
                arr1[k--] = arr2[j--];
            }
        }
        
        while (j >= 0) {
            arr1[k--] = arr2[j--];
        }
    }
}
```

## Conclusion

In this blog post, we explored two approaches for merging two sorted arrays in Java. The first approach involves using extra space to create a new merged array, while the second approach performs an in-place merge, optimizing the space complexity. Both approaches can be used depending on the requirements and constraints of the application.

You can find the complete code examples in the [MergeSortedArrays](https://github.com/example/MergeSortedArrays) repository.

#java #sorting