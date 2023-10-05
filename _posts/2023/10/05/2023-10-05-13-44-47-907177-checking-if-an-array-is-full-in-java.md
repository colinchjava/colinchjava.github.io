---
layout: post
title: "Checking if an array is full in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---
In Java, arrays have a fixed size once they are created. It is important to check if an array is full before adding any elements to avoid `ArrayIndexOutOfBoundsException`.

## Method 1: Using Array Length

One way to check if an array is full is by comparing the length of the array to the maximum capacity. Here's an example:

```java
int[] numbers = new int[5];
boolean isFull = numbers.length == 5;
```

In this example, we have created an array called `numbers` with a maximum capacity of 5. By checking if `numbers.length` is equal to 5, we can determine if the array is full.

## Method 2: Using a Variable

Another approach is to keep track of the number of filled positions in the array using a separate variable. Here's an example:

```java
int[] numbers = new int[5];
int count = 0;

// Adding elements to the array
numbers[count++] = 10;
numbers[count++] = 20;
numbers[count++] = 30;
numbers[count++] = 40;

boolean isFull = count == numbers.length;
```

In this example, we initialize an array called `numbers` with a capacity of 5 and create a variable `count` to track the number of elements added to the array. After adding elements to the array, we check if `count` is equal to `numbers.length` to determine if the array is full.

## Conclusion
Checking if an array is full is an essential step to avoid accessing invalid indices. Whether you choose to compare the array length or use a separate variable, both methods will help you determine if an array is full in Java.

#java #programming