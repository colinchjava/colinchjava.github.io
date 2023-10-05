---
layout: post
title: "Copying a Java array to another array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

## Method 1: Using a for loop

One way to copy a Java array to another array is by iterating over each element of the source array and manually copying it to the destination array using a for loop. Here's an example to illustrate this method:

```java
// Source array
int[] sourceArray = { 1, 2, 3, 4, 5 };

// Destination array
int[] destinationArray = new int[sourceArray.length];

// Copying elements using a for loop
for (int i = 0; i < sourceArray.length; i++) {
    destinationArray[i] = sourceArray[i];
}
```

In the above code snippet, we create a source array with some elements. Then, we create a destination array of the same length as the source array. Next, we iterate over each element of the source array using a for loop and copy it to the corresponding index in the destination array.

## Method 2: Using System.arraycopy()

Another way to copy a Java array to another array is by using the `System.arraycopy()` method. This method provides a more concise and efficient way to copy arrays. Here's an example to demonstrate this method:

```java
// Source array
int[] sourceArray = { 1, 2, 3, 4, 5 };

// Destination array
int[] destinationArray = new int[sourceArray.length];

// Copying elements using System.arraycopy()
System.arraycopy(sourceArray, 0, destinationArray, 0, sourceArray.length);
```

In the above code snippet, we use the `System.arraycopy()` method to copy the elements from the source array to the destination array. The method takes the source array, the starting position in the source array, the destination array, the starting position in the destination array, and the number of elements to be copied.

Both methods mentioned above will create a separate copy of the source array. Any modifications made to the destination array will not affect the original source array.

By using either the for loop or the `System.arraycopy()` method, you can easily copy a Java array to another array. Choose the method that suits your requirements and coding style. Happy coding!

----------

Tags: Java, arrays