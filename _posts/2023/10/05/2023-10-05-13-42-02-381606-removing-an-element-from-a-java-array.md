---
layout: post
title: "Removing an element from a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, arrays have a fixed size and removing elements from an array requires shifting all the subsequent elements to fill up the empty space. This can be a bit tricky, but with proper understanding and implementation, it can be achieved with ease. In this blog post, we will explore different techniques to remove an element from a Java array.

## Table of Contents
- [Using ArrayList](#Using-ArrayList)
- [Using System.arraycopy](#Using-System-arraycopy)

## Using ArrayList

One of the easiest ways to remove an element from a Java array is by using the `ArrayList` class from the `java.util` package. `ArrayList` provides an easy way to dynamically manage the size of the array-like structure.

Here's an example of how to remove an element from an array using `ArrayList`:

```java
import java.util.ArrayList;

public class ArrayRemovalExample {
    public static void main(String[] args) {
        int[] numbers = { 1, 2, 3, 4, 5 };
        
        ArrayList<Integer> list = new ArrayList<>();
        for (int num : numbers) {
            list.add(num);
        }
        
        list.remove(2); // Remove element at index 2

        // Convert the ArrayList back to an array
        numbers = list.toArray(new int[0]);

        for (int num : numbers) {
            System.out.println(num);
        }
    }
}
```

In this example, we create an `ArrayList` named `list` and iterate over the original array to add each element to the list. Then, we simply call the `remove` method on the `ArrayList` to remove the desired element at the specified index (in this case, index 2). Finally, we convert the `ArrayList` back to an array by using the `toArray` method and assign it to the original array.

## Using System.arraycopy
Another approach to removing an element from a Java array is by using `System.arraycopy` method, which allows you to copy elements from one array to another. By leveraging this method, we can overwrite the element to be removed with the subsequent elements in the array.

Here's an example:

```java
public class ArrayRemovalExample {
    public static void main(String[] args) {
        int[] numbers = { 1, 2, 3, 4, 5 };
        int indexToRemove = 2;

        // Shift the elements after the index to be removed
        System.arraycopy(numbers, indexToRemove + 1, numbers, indexToRemove, numbers.length - indexToRemove - 1);

        // Resize the array by creating a new array with the desired length
        int[] resizedArray = new int[numbers.length - 1];
        System.arraycopy(numbers, 0, resizedArray, 0, resizedArray.length);

        for (int num : resizedArray) {
            System.out.println(num);
        }
    }
}
```

In this example, we use `System.arraycopy` to shift the elements after the index to be removed. The length of the destination array is reduced to exclude the removed element. Finally, we create a new array of the desired length and copy the elements from the original array to the resized array.

Both approaches discussed in this blog post provide ways to remove elements from a Java array. While the `ArrayList` approach is more intuitive and flexible, the `System.arraycopy` approach allows you to modify the original array directly without the need for an intermediate data structure. Depending on the situation, you can choose the appropriate technique that best suits your requirements.

#java #array #removal