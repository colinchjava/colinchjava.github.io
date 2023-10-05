---
layout: post
title: "Finding the difference between two arrays in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with arrays in Java, you may need to find the difference between two arrays, i.e., the elements that are present in one array but not in the other. In this blog post, we will explore different approaches to accomplish this task.

## Method 1: Using Two Nested Loops

One way to find the difference between two arrays is by using two nested loops. Here's an example code snippet in Java:

```java
public static int[] findDifference(int[] array1, int[] array2) {
    int[] result = new int[array1.length];
    int count = 0;

    for (int i = 0; i < array1.length; i++) {
        boolean found = false;

        for (int j = 0; j < array2.length; j++) {
            if (array1[i] == array2[j]) {
                found = true;
                break;
            }
        }

        if (!found) {
            result[count++] = array1[i];
        }
    }

    return Arrays.copyOf(result, count);
}
```
In this method, we iterate over each element of the first array, and for each element, we iterate over the second array to check if it exists. If an element from the first array is not found in the second array, we add it to the result array.

## Method 2: Using HashSet

An efficient way to find the difference between two arrays is by using a HashSet data structure. Here's an example code snippet:

```java
public static int[] findDifference(int[] array1, int[] array2) {
    Set<Integer> set = new HashSet<>();

    for (int num : array2) {
        set.add(num);
    }

    List<Integer> resultList = new ArrayList<>();
    for (int num : array1) {
        if (!set.contains(num)) {
            resultList.add(num);
        }
    }

    return resultList.stream().mapToInt(Integer::intValue).toArray();
}
```

In this method, we first add all the elements of the second array into a HashSet. Then, we iterate over the first array and check if each element exists in the HashSet. If not, we add it to a resultList. Finally, we convert the resultList into an array.

## Conclusion

In this blog post, we explored two different approaches to find the difference between two arrays in Java. You can choose the method that best suits your requirements. Whether you prefer using nested loops or HashSet for better performance, these methods can help you efficiently find the difference between arrays in your Java programs.

#java #arrays