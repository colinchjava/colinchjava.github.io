---
layout: post
title: "Counting occurrences of elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with arrays in Java, it's common to need to count the number of occurrences of each element within the array. This can be useful for various tasks, such as finding the most frequent element or checking if a certain element appears a specific number of times.

In this article, we will explore different approaches to count the occurrences of elements in a Java array.

### Method 1: Using a HashMap

One way to count the occurrences of elements in a Java array is by using a `HashMap`. Here's an example:

```java
import java.util.HashMap;
import java.util.Map;

public class ArrayElementCounter {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 2, 1, 3, 4, 5, 1};

        Map<Integer, Integer> countMap = new HashMap<>();

        for (int element : array) {
            if (countMap.containsKey(element)) {
                countMap.put(element, countMap.get(element) + 1);
            } else {
                countMap.put(element, 1);
            }
        }

        // Print the occurrences of each element
        for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
            System.out.println("Element " + entry.getKey() + " occurs " + entry.getValue() + " times");
        }
    }
}
```

In this code, we iterate over the array and use a `HashMap` to store the count of each element. If the element is already present in the map, we increment its count by 1. Otherwise, we add it to the map with a count of 1. Finally, we iterate over the map and print the occurrences of each element.

### Method 2: Using an Array

Another approach to count the occurrences of elements in a Java array is by using an additional array to store the counts. Here's an example:

```java
public class ArrayElementCounter {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 2, 1, 3, 4, 5, 1};
        int[] countArray = new int[array.length];

        for (int i = 0; i < array.length; i++) {
            int count = 1;

            for (int j = i + 1; j < array.length; j++) {
                if (array[i] == array[j]) {
                    count++;
                }
            }

            if (countArray[i] == 0) {
                countArray[i] = count;
            }
        }

        // Print the occurrences of each element
        for (int i = 0; i < array.length; i++) {
            if (countArray[i] > 0) {
                System.out.println("Element " + array[i] + " occurs " + countArray[i] + " times");
            }
        }
    }
}
```

In this code, we initialize an additional array with the same length as the input array to store the counts. We iterate over the input array and for each element, we count its occurrences by iterating over the remaining elements. We then store the count in the corresponding index of the count array. Finally, we iterate over the count array and print the occurrences of each element.

### Conclusion

Counting the occurrences of elements in a Java array can be achieved using different approaches. By leveraging the power of `HashMap` or using an additional array, you can easily count and analyze the frequency of elements in an array. Choose the approach that suits your specific use case and enjoy efficient array element counting in your Java programs.

#java #array #count #elements