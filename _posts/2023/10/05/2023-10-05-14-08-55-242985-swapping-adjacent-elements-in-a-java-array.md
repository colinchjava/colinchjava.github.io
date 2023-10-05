---
layout: post
title: "Swapping adjacent elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, it is often necessary to swap adjacent elements in an array. This can be useful for various tasks, such as sorting algorithms or reordering elements. In this blog post, we will discuss how to swap adjacent elements in a Java array efficiently.

### Approach

To swap adjacent elements in a Java array, we can use a simple loop that iterates through the array and swaps each pair of adjacent elements. Here's an example implementation:

```java
public class ArraySwap {
    public static void swapAdjacentElements(int[] arr) {
        for (int i = 0; i < arr.length - 1; i += 2) {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }
    }
}
```

In the `swapAdjacentElements` method, we use a `for` loop to iterate through the array. We initialize the loop variable `i` to 0 and increment it by 2 in each iteration. This ensures that we only swap adjacent elements.

Inside the loop, we use a temporary variable `temp` to store the value of the current element `arr[i]`. Then, we assign the value of the next element `arr[i + 1]` to `arr[i]`, and finally assign the value of `temp` to `arr[i + 1]`.

### Usage

To use the `swapAdjacentElements` method, we can create an instance of the `ArraySwap` class and call the method with our array as an argument. Here's an example:

```java
public class Main {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5};
        ArraySwap.swapAdjacentElements(array);
        
        for (int num : array) {
            System.out.print(num + " ");
        }
    }
}
```

The output of the above code will be:

```
2 1 4 3 5
```

As you can see, the adjacent elements in the array have been swapped.

### Conclusion

Swapping adjacent elements in a Java array can be achieved by iterating through the array and swapping each pair of adjacent elements. This approach is simple and efficient, and can be useful in various scenarios.