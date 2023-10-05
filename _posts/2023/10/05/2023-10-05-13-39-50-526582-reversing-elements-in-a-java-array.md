---
layout: post
title: "Reversing elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, if you have an array and you want to reverse the order of its elements, you can do so by iterating through the array and swapping the elements at the corresponding positions.

Here's an example of how to reverse the elements in a Java array:

```java
public class ArrayReverseExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};

        System.out.println("Original array: " + Arrays.toString(numbers));

        int start = 0;
        int end = numbers.length - 1;
        while (start < end) {
            int temp = numbers[start];
            numbers[start] = numbers[end];
            numbers[end] = temp;
            start++;
            end--;
        }

        System.out.println("Reversed array: " + Arrays.toString(numbers));
    }
}
```

In this example, we start by initializing an array `numbers` with some values. Then, we print the original array using `Arrays.toString()`.

We use two variables: `start` and `end`, which point to the beginning and end of the array, respectively. 

Inside the while loop, we swap the elements at `start` and `end` positions using a temporary variable `temp`. We increment `start` and decrement `end` after each swap.

The loop continues until `start` becomes greater than or equal to `end`, ensuring that we reverse all the elements in the array.

Finally, we print the reversed array using `Arrays.toString()`.

When you run this code, the output will be:

```
Original array: [1, 2, 3, 4, 5]
Reversed array: [5, 4, 3, 2, 1]
```

By reversing the elements in a Java array, you can easily manipulate the order of elements to suit your needs.