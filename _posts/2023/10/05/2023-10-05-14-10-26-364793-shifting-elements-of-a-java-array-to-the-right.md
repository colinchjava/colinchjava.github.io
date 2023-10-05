---
layout: post
title: "Shifting elements of a Java array to the right"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this blog post, we'll explore how to shift elements of a Java array to the right. Shifting elements can be useful in scenarios where you want to reposition elements within the array or create space for new elements.

## Table of Contents
- [Approach 1: Using an Auxiliary Array](#approach-1-using-an-auxiliary-array)
- [Approach 2: Using Reverse Reassignment](#approach-2-using-reverse-reassignment)

## Approach 1: Using an Auxiliary Array
One way to shift elements of an array to the right is by using an auxiliary array. Here's how you can implement this approach:

```java
public static void shiftElements(int[] arr, int k) {
    int n = arr.length;
    int[] aux = new int[n];

    for (int i = 0; i < n; i++) {
        aux[(i + k) % n] = arr[i];
    }

    for (int i = 0; i < n; i++) {
        arr[i] = aux[i];
    }
}
```

In the code above:
- We create an auxiliary array of the same size as the original array.
- We iterate over each element of the original array and assign it to the corresponding index in the auxiliary array, shifted by `k` positions to the right using the modulus operator.
- Finally, we update the original array with the values from the auxiliary array.

Here's an example usage of the `shiftElements` method:

```java
int[] arr = {1, 2, 3, 4, 5};
int k = 2;
shiftElements(arr, k);
System.out.println(Arrays.toString(arr));
```

Output:
```
[4, 5, 1, 2, 3]
```

## Approach 2: Using Reverse Reassignment
Another approach to shift elements of an array to the right is by using reverse reassignment. Here's a code snippet that demonstrates this approach:

```java
public static void shiftElements(int[] arr, int k) {
    int n = arr.length;

    // Reverse the entire array
    reverse(arr, 0, n - 1);

    // Reverse the first k elements
    reverse(arr, 0, k - 1);

    // Reverse the remaining n-k elements
    reverse(arr, k, n - 1);
}

public static void reverse(int[] arr, int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}
```

In the code above:
- The `shiftElements` method first reverses the entire array.
- It then reverses the first `k` elements.
- Finally, it reverses the remaining `n-k` elements.

Here's an example usage of the `shiftElements` method:

```java
int[] arr = {1, 2, 3, 4, 5};
int k = 2;
shiftElements(arr, k);
System.out.println(Arrays.toString(arr));
```

Output:
```
[4, 5, 1, 2, 3]
```

## Conclusion
Shifting elements of a Java array to the right can be accomplished using various techniques. In this blog post, we explored two approaches: using an auxiliary array and using reverse reassignment. Depending on your specific requirements, you can choose the approach that best suits your needs.

#java #arrays