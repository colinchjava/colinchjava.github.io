---
layout: post
title: "Accessing elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, an array is a collection of elements of the same type, which are stored in a contiguous memory location. To access elements in an array, you need to know the index of the element you want to access. 

Here's an example of how to access elements in a Java array:

```java
// Declare and initialize an array of integers
int[] numbers = { 10, 20, 30, 40, 50 };

// Access the first element in the array
int firstElement = numbers[0];
System.out.println("First element: " + firstElement);

// Access the third element in the array
int thirdElement = numbers[2];
System.out.println("Third element: " + thirdElement);

// Change the value of the last element in the array
numbers[numbers.length - 1] = 60;
System.out.println("Last element: " + numbers[numbers.length - 1]);
```

In the above example, we have an array called `numbers` with five elements. To access an element in the array, we use the square bracket notation `[]`, followed by the index of the element we want to access. Remember that array indices start from 0, so the first element has an index of 0, the second element has an index of 1, and so on.

We can also assign a new value to an element in the array by using the same square bracket notation. In the example above, we change the value of the last element in the array to 60.

Make sure to be mindful of the array bounds when accessing elements. Trying to access an element outside the bounds of the array will result in an `ArrayIndexOutOfBoundsException`.