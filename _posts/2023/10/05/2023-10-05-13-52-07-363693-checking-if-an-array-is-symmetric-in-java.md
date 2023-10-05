---
layout: post
title: "Checking if an array is symmetric in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Array is one of the fundamental data structures in programming. It allows us to store multiple values of the same data type in a single variable. In this blog post, we are going to discuss how to check if an array is symmetric in Java.

## What is a Symmetric Array?

A symmetric array is an array where the elements at corresponding positions from the start and end of the array are equal. In other words, if we reverse the array and the reversed array is the same as the original array, the array is considered symmetric.

## Approach to Check Symmetric Array

To check if an array is symmetric, we can compare the elements at corresponding positions from the start and end of the array. If they are equal, we continue to check the next pair. If any pair of elements is not equal, the array is not symmetric. The algorithm can be summarized as follows:

1. Initialize two pointers, `start` and `end`, pointing to the first and last elements of the array, respectively.
2. Iterate through the array until `start` is less than or equal to `end`.
3. Compare the values at `array[start]` and `array[end]`.
4. If the values are not equal, the array is not symmetric and we exit the loop.
5. Increment `start` and decrement `end` by 1.
6. Repeat steps 3-5 until `start` is less than or equal to `end`.
7. If we successfully iterate through the entire array without encountering any non-matching pairs, the array is symmetric.

## Checking Symmetric Array in Java

Here is an example Java function that checks if an array is symmetric:

```java
public class SymmetricArrayChecker {
    public static boolean isSymmetric(int[] array) {
        int start = 0;
        int end = array.length - 1;
        
        while (start <= end) {
            if (array[start] != array[end]) {
                return false;
            }
            
            start++;
            end--;
        }
        
        return true;
    }
}
```

To use this function, simply pass an integer array to the `isSymmetric` method, and it will return `true` if the array is symmetric, and `false` otherwise.

## Example Usage

```java
int[] symmetricArray = {1, 2, 3, 2, 1};
int[] nonSymmetricArray = {1, 2, 3, 4, 5};

boolean isSymmetricArray = SymmetricArrayChecker.isSymmetric(symmetricArray);
boolean isNonSymmetricArray = SymmetricArrayChecker.isSymmetric(nonSymmetricArray);

System.out.println("Is symmetricArray symmetric? " + isSymmetricArray);
System.out.println("Is nonSymmetricArray symmetric? " + isNonSymmetricArray);
```

## Conclusion

In this blog post, we have discussed how to check if an array is symmetric in Java. We have presented an algorithm and provided an example Java function that implements this algorithm. By using this approach, you can easily determine if an array is symmetric or not.

#java #arrays