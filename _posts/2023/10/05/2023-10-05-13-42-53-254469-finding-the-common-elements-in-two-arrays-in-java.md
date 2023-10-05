---
layout: post
title: "Finding the common elements in two arrays in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with arrays in Java, you might come across a scenario where you need to find the common elements between two arrays. In this blog post, we'll explore different approaches to achieve this task efficiently.

## Approach 1: Using Nested Loops

One straightforward approach to find the common elements is by using nested loops. Here's an example code snippet:

```java
import java.util.Arrays;

public class CommonElements {
    public static void main(String[] args) {
        int[] array1 = {1, 2, 3, 4, 5};
        int[] array2 = {4, 5, 6, 7, 8};

        System.out.println("Common elements:");
        for (int i = 0; i < array1.length; i++) {
            for (int j = 0; j < array2.length; j++) {
                if (array1[i] == array2[j]) {
                    System.out.println(array1[i]);
                    break;
                }
            }
        }
    }
}
```

In this approach, we use two nested loops to iterate over each element of both arrays. We compare each element from the first array with every element in the second array. If a common element is found, we print it out.

## Approach 2: Using HashSet

Another efficient approach to find common elements is by utilizing a HashSet. Here's an example code snippet:

```java
import java.util.Arrays;
import java.util.HashSet;

public class CommonElements {
    public static void main(String[] args) {
        int[] array1 = {1, 2, 3, 4, 5};
        int[] array2 = {4, 5, 6, 7, 8};

        HashSet<Integer> set1 = new HashSet<>();
        for (int num : array1) {
            set1.add(num);
        }

        System.out.println("Common elements:");
        for (int num : array2) {
            if (set1.contains(num)) {
                System.out.println(num);
            }
        }
    }
}
```

In this approach, we create a HashSet and add all elements from the first array to it. Then, we iterate over the second array and check if each element exists in the HashSet. If it does, we print it out as a common element.

## Conclusion

Both approaches mentioned above are efficient ways to find the common elements between two arrays in Java. However, the second approach using HashSet offers better time complexity, especially for larger arrays. It eliminates the need for nested loops, resulting in a more optimized solution.

Remember to choose the approach based on the specific requirements of your application and consider factors such as array size and desired time complexity.

Happy coding!

\#Java #Arrays