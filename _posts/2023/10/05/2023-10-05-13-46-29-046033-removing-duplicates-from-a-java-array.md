---
layout: post
title: "Removing duplicates from a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In many programming scenarios, we may need to remove duplicate elements from an array to ensure the uniqueness of its contents. Java offers several approaches to accomplish this task efficiently. In this blog post, we will explore some of the common methods to remove duplicates from a Java array.

## Method 1: Using a Set

One of the easiest and most efficient ways to remove duplicates from an array is by using a `Set`. A `Set` in Java guarantees that it will only hold unique elements. Here's an example of how to remove duplicates using a `Set`:

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

public class ArrayDuplicateRemoval {
    public static void main(String[] args) {
        Integer[] array = {1, 2, 3, 4, 3, 2, 1}; // Example array with duplicates

        Set<Integer> uniqueSet = new HashSet<>(Arrays.asList(array));
        Integer[] uniqueArray = uniqueSet.toArray(new Integer[0]);

        System.out.println(Arrays.toString(uniqueArray));
    }
}
```

In the code above, we convert the array to a `Set` using `Arrays.asList(array)` and then convert it back to an array using `toArray()`. This effectively removes duplicates from the array.

## Method 2: Using ArrayList

Another approach is to use an `ArrayList` to remove duplicates. Here's an example:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ArrayDuplicateRemoval {
    public static void main(String[] args) {
        Integer[] array = {1, 2, 3, 4, 3, 2, 1}; // Example array with duplicates

        List<Integer> uniqueList = new ArrayList<>();
        for (Integer element : array) {
            if (!uniqueList.contains(element)) {
                uniqueList.add(element);
            }
        }

        Integer[] uniqueArray = uniqueList.toArray(new Integer[0]);

        System.out.println(Arrays.toString(uniqueArray));
    }
}
```

In this code, we iterate over each element in the array and add it to the `ArrayList` if it does not already exist in the list.

## Method 3: Using Java 8 Streams

If you are using Java 8 or higher, you can take advantage of the `distinct()` method available in Java streams to remove duplicates in a concise and elegant way:

```java
import java.util.Arrays;

public class ArrayDuplicateRemoval {
    public static void main(String[] args) {
        Integer[] array = {1, 2, 3, 4, 3, 2, 1}; // Example array with duplicates

        Integer[] uniqueArray = Arrays.stream(array).distinct().toArray(Integer[]::new);

        System.out.println(Arrays.toString(uniqueArray));
    }
}
```

By using the `distinct()` method in the stream, we ensure that the resulting stream contains only unique elements. Finally, we convert the stream back to an array using the `toArray()` method.

## Conclusion

In this blog post, we explored three different methods to remove duplicates from a Java array. The first method uses a `Set` to ensure uniqueness, the second method utilizes an `ArrayList` to filter out duplicates, and the third method leverages Java 8 streams to achieve the same result in a concise manner. Choose the method that best suits your needs and coding style.

#java #arrays