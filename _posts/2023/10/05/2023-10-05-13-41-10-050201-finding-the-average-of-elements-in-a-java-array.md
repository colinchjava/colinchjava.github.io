---
layout: post
title: "Finding the average of elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, you might often need to calculate the average of elements in an array. In this blog post, we will explore different approaches to finding the average of an array in Java.

## Method 1: Using a For Loop

One way to calculate the average of elements in an array is by using a for loop. Here's an example code snippet that demonstrates this method:

```java
public class AverageCalculator {
    public static double calculateAverage(int[] array) {
        int sum = 0;

        for (int i = 0; i < array.length; i++) {
            sum += array[i];
        }

        return (double) sum / array.length;
    }

    public static void main(String[] args) {
        int[] numbers = { 5, 10, 15, 20, 25 };
        double average = calculateAverage(numbers);

        System.out.println("The average is: " + average);
    }
}
```

In this code, we have a method `calculateAverage` that takes an array of integers as a parameter. Inside the method, we use a for loop to iterate over the array and calculate the sum of all elements. We then divide the sum by the length of the array to get the average.

## Method 2: Using Java Stream API

In Java 8 and above, you can use the Stream API to calculate the average of elements in an array in a more concise way. Here's an example code snippet that demonstrates this method:

```java
import java.util.Arrays;

public class AverageCalculator {
    public static double calculateAverage(int[] array) {
        return Arrays.stream(array)
                .average()
                .orElse(0);
    }

    public static void main(String[] args) {
        int[] numbers = { 5, 10, 15, 20, 25 };
        double average = calculateAverage(numbers);

        System.out.println("The average is: " + average);
    }
}
```

In this code, we use the `Arrays.stream()` method to convert the array into a stream of elements. Then, we can simply call the `average()` method on the stream to calculate the average. The `orElse()` method is used to handle the case when the array is empty.

## Conclusion

Finding the average of elements in a Java array can be accomplished using different methods. You can choose between using a for loop or leveraging the Stream API introduced in Java 8. Both methods provide an effective way to calculate the average, so pick the one that suits your coding style and requirements.

#java #arrays