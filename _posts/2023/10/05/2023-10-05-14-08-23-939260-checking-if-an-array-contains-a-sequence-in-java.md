---
layout: post
title: "Checking if an array contains a sequence in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

## Method 1: Using a for loop

```java
public static boolean containsSequence(int[] array, int[] sequence) {
    for (int i = 0; i <= array.length - sequence.length; i++) {
        boolean found = true;
        for (int j = 0; j < sequence.length; j++) {
            if (array[i + j] != sequence[j]) {
                found = false;
                break;
            }
        }
        if (found) {
            return true;
        }
    }
    return false;
}
```

Here, we iterate over the array using a for loop and check if each element of the sequence matches the corresponding element in the array. If at any point the elements don't match, we break out of the inner loop and move on to the next index of the array. If we find a match for all elements of the sequence, we return `true`. Otherwise, we continue checking until the end of the array and return `false` if we don't find a match.

## Method 2: Using `Arrays.copyOfRange()`

```java
public static boolean containsSequence(int[] array, int[] sequence) {
    for (int i = 0; i <= array.length - sequence.length; i++) {
        int[] subArray = Arrays.copyOfRange(array, i, i + sequence.length);
        if (Arrays.equals(subArray, sequence)) {
            return true;
        }
    }
    return false;
}
```

In this method, we use the `Arrays.copyOfRange()` method to create a sub-array from the main array, starting from each index and having the length of the sequence. We then use the `Arrays.equals()` method to check if the sub-array matches the sequence. If we find a match, we return `true`. Otherwise, we continue checking until the end of the array and return `false` if we don't find a match.

## Method 3: Using `String` manipulation

```java
public static boolean containsSequence(int[] array, int[] sequence) {
    String arrayString = Arrays.toString(array);
    String sequenceString = Arrays.toString(sequence);
    return arrayString.contains(sequenceString);
}
```

In this method, we convert both the array and sequence into strings using `Arrays.toString()` method. Then, we use the `contains()` method of the `String` class to check if the array string contains the sequence string. If it does, we return `true`, otherwise `false`.

## Conclusion

In this blog post, we explored three different methods to check if an array contains a sequence in Java. Each method has its own advantages and disadvantages and you can choose the one that suits your requirements and coding style. Remember to consider the size of the arrays and the time complexity of the methods when dealing with large data sets. Happy coding!

\#java #programming