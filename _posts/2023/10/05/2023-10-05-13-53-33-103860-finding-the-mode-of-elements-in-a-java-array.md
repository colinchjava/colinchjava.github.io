---
layout: post
title: "Finding the mode of elements in a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In statistics, the mode refers to the value that appears most frequently in a dataset. If you have an array of elements in Java and you want to find the mode, you can follow a simple approach using a HashMap.

Here's a step-by-step guide on how to find the mode of elements in a Java array:

## Step 1: Import the required packages
```java
import java.util.HashMap;
import java.util.Map;
```

## Step 2: Define a method to find the mode
```java
public static int findMode(int[] array) {
    // Create a HashMap to store the frequency of each element
    HashMap<Integer, Integer> frequencyMap = new HashMap<>();

    // Loop through the array and count the frequency of each element
    for (int num : array) {
        frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
    }

    // Find the element with the highest frequency
    int mode = 0;
    int maxFrequency = 0;
    for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
        int frequency = entry.getValue();
        if (frequency > maxFrequency) {
            mode = entry.getKey();
            maxFrequency = frequency;
        }
    }

    return mode;
}
```

## Step 3: Test the method
```java
public static void main(String[] args) {
    int[] array = {1, 2, 3, 4, 4, 5, 5, 5};
    int mode = findMode(array);
    
    System.out.println("The mode of the array is: " + mode);
}
```

## Explanation

1. We start by importing the required packages, `java.util.HashMap` and `java.util.Map`, which are needed to create a HashMap and iterate over its entries.

2. We define a method named `findMode` that takes an integer array as input and returns the mode as an integer.

3. Inside the `findMode` method, we create a HashMap named `frequencyMap` to store the frequency of each element in the array.

4. Next, we loop through the array and use the `getOrDefault` method of `frequencyMap` to count the frequency of each element. If the element is already present in the map, we increment its frequency by 1. If the element is not present, we set its frequency to 1.

5. After counting the frequency of each element, we loop over the entries of `frequencyMap` using a `for-each` loop.

6. Inside the loop, we compare the frequency of each element with the maximum frequency seen so far. If the current frequency is greater than the maximum frequency, we update the `mode` variable to hold the current element, and update the `maxFrequency` variable with the new maximum frequency.

7. Finally, we return the `mode` value as the result of the method.

8. In the `main` method, we create an example array and call the `findMode` method to get the mode. We then print the mode to the console.

By following these steps, you can easily find the mode of elements in a Java array using a HashMap.