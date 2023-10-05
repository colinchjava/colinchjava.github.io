---
layout: post
title: "Reversing words in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we will discuss how to reverse the order of words in a Java array. We will explore a simple and efficient approach to achieve this using only a few lines of code.

## Table of Contents
- [Introduction](#introduction)
- [Approach](#approach)
- [Implementation](#implementation)
- [Conclusion](#conclusion)

## Introduction
Imagine you have an array of words in Java, and you want to reverse the order of those words. For example, if the original array is `["Hello", "World", "Java"]`, after reversing the order, the array should become `["Java", "World", "Hello"]`. 

## Approach
To reverse the order of words in a Java array, we can use a two-pointer technique. We will start with two pointers, one pointing to the beginning of the array and the other pointing to the end. We will swap the words pointed by both the pointers and increment the first pointer and decrement the second pointer until they meet in the middle.

## Implementation
Let's see how we can implement this approach in Java:

```java
public class ArrayWordReversal {
    public static void reverseWords(String[] words) {
        int start = 0;
        int end = words.length - 1;

        while (start < end) {
            // Swap words at start and end pointers
            String temp = words[start];
            words[start] = words[end];
            words[end] = temp;

            // Move pointers towards the middle
            start++;
            end--;
        }
    }
    
    public static void main(String[] args) {
        String[] words = {"Hello", "World", "Java"};
        
        System.out.println("Original Array: " + Arrays.toString(words));
        reverseWords(words);
        System.out.println("Reversed Array: " + Arrays.toString(words));
    }
}
```

In the above code, we define a `reverseWords` method that takes an array of Strings as input and performs the reversal. We initialize the `start` and `end` pointers to the first and last indices of the array, respectively. Then, using a `while` loop, we swap the words at the `start` and `end` pointers and move the pointers towards the middle until they meet.

In the `main` method, we create a sample array of words and call the `reverseWords` method to reverse the order of words. Finally, we print the original and reversed arrays to verify the correctness of our implementation.

## Conclusion
In this blog post, we explored how to reverse the order of words in a Java array. We learned a simple and efficient approach using a two-pointer technique. By swapping words at the start and end pointers and moving the pointers towards the middle, we were able to achieve the desired reversal. This technique can be useful in various scenarios where word rearrangement is required.