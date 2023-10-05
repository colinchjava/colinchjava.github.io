---
layout: post
title: "Checking if an array contains only unique elements in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

## Method 1: Using a Set
One simple way to check if an array contains only unique elements is by converting the array into a Set. If the size of the Set is equal to the size of the array, then all elements in the array are unique.

Here is an example code snippet that demonstrates this approach:

```java
import java.util.*;

public class UniqueArrayChecker {
    public static boolean containsOnlyUniqueElements(int[] array) {
        Set<Integer> set = new HashSet<>();
        for (int num : array) {
            if (!set.add(num)) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5};
        boolean isUnique = containsOnlyUniqueElements(array);
        System.out.println("Is the array unique? " + isUnique);
    }
}
```

## Method 2: Sorting the Array
Another approach is to sort the array and then check if any adjacent elements are equal. If we find any equal adjacent elements, it means the array contains duplicates.

Here is an example code snippet that demonstrates this approach:

```java
import java.util.Arrays;

public class UniqueArrayChecker {
    public static boolean containsOnlyUniqueElements(int[] array) {
        Arrays.sort(array);
        for (int i = 0; i < array.length - 1; i++) {
            if (array[i] == array[i + 1]) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        int[] array = {1, 2, 3, 3, 4};
        boolean isUnique = containsOnlyUniqueElements(array);
        System.out.println("Is the array unique? " + isUnique);
    }
}
```

## Method 3: Comparing Each Element
A third approach is to compare each element in the array with all the other elements. If we find any equal elements while comparing, it means the array contains duplicates.

Here is an example code snippet that demonstrates this approach:

```java
public class UniqueArrayChecker {
    public static boolean containsOnlyUniqueElements(int[] array) {
        for (int i = 0; i < array.length; i++) {
            for (int j = i + 1; j < array.length; j++) {
                if (array[i] == array[j]) {
                    return false;
                }
            }
        }
        return true;
    }

    public static void main(String[] args) {
        int[] array = {1, 2, 3, 3, 4};
        boolean isUnique = containsOnlyUniqueElements(array);
        System.out.println("Is the array unique? " + isUnique);
    }
}
```

## Conclusion
In this blog post, we explored three different methods to check if an array contains only unique elements in Java. You can choose the method that suits your requirements. However, using a Set is generally the most efficient approach. Remember to take into account the size and complexity of the array when choosing the method.

**#Java #Arrays**