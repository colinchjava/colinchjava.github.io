---
layout: post
title: "Finding the index of the first occurrence of an element in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we will discuss how to find the index of the first occurrence of an element in a Java array. This can be a common task when working with arrays and searching for a specific value.

Let's assume we have an array of integers called `numbers` and we want to find the index of the first occurrence of a specific value, `targetValue`.

## Implementing a linear search

One way to solve this problem is by implementing a *linear search* algorithm. Here's an example code snippet that demonstrates how to do this:

```java
public static int findFirstOccurrence(int[] array, int target) {
    for (int i = 0; i < array.length; i++) {
        if (array[i] == target) {
            return i;
        }
    }
    return -1; // If the element is not found
}
```

In this code, we iterate over each element of the array using a for loop. We compare each element with the target value, and if a match is found, we immediately return the index `i`. If the element is not found, we return -1.

## Testing the code with a sample array

Let's test our code using a sample array and a target value to see if it returns the correct index. Consider the following code snippet:

```java
public static void main(String[] args) {
    int[] numbers = { 5, 8, 2, 9, 3, 6 };
    int targetValue = 9;
    int index = findFirstOccurrence(numbers, targetValue);
    if (index != -1) {
        System.out.println("The first occurrence of " + targetValue + " is at index " + index);
    } else {
        System.out.println("The element " + targetValue + " is not found in the array");
    }
}
```

This code creates an array `numbers` and sets the `targetValue` to 9. It then calls the `findFirstOccurrence` method and prints the result.

When running this code, we should see the following output:

```
The first occurrence of 9 is at index 3
```

## Conclusion

In this blog post, we covered a common task: finding the index of the first occurrence of an element in a Java array. We implemented a linear search algorithm to solve this problem and demonstrated how to test the code with a sample array.

Remember, the linear search algorithm has a time complexity of O(n) in the worst case, where n is the size of the array. For large arrays, considering using more efficient search algorithms like binary search.