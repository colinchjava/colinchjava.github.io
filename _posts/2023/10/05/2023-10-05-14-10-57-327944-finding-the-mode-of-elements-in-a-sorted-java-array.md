---
layout: post
title: "Finding the mode of elements in a sorted Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In this article, we will discuss how to find the mode of elements in a sorted Java array using two different approaches. The mode of a set of elements is the value(s) that appear(s) most frequently in the set. 

## Table of Contents
1. [Using a Linear Scan Approach](#using-a-linear-scan-approach)
2. [Using a HashMap Approach](#using-a-hashmap-approach)
3. [Conclusion](#conclusion)

## Using a Linear Scan Approach

The linear scan approach involves iterating through the sorted array and keeping track of the frequencies of each element. 

Here's an example code snippet that demonstrates this approach:

```java
public static int findMode(int[] array) {
    int mode = array[0];
    int maxFrequency = 1;
  
    int currentFrequency = 1;
    int currentElement = array[0];
  
    for (int i = 1; i < array.length; i++) {
        if (array[i] == currentElement) {
            currentFrequency++;
        } else {
            if (currentFrequency > maxFrequency) {
                maxFrequency = currentFrequency;
                mode = currentElement;
            }
            currentElement = array[i];
            currentFrequency = 1;
        }
    }
  
    // Check for mode at the end of the array
    if (currentFrequency > maxFrequency) {
        mode = currentElement;
    }
  
    return mode;
}
```

In this approach, we initialize `mode` and `maxFrequency` variables with the first element of the array. We also maintain `currentFrequency` and `currentElement` variables to keep track of the current element and its frequency while iterating through the array.

## Using a HashMap Approach

Another approach to finding the mode of elements in a sorted Java array is using a HashMap to store the frequencies of each element.

Here's an example code snippet that demonstrates this approach:

```java
import java.util.HashMap;
import java.util.Map;

public static int findMode(int[] array) {
    Map<Integer, Integer> frequencyMap = new HashMap<>();
  
    for (int i = 0; i < array.length; i++) {
        frequencyMap.put(array[i], frequencyMap.getOrDefault(array[i], 0) + 1);
    }
  
    int mode = 0;
    int maxFrequency = 0;
  
    for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
        if (entry.getValue() > maxFrequency) {
            maxFrequency = entry.getValue();
            mode = entry.getKey();
        }
    }
  
    return mode;
}
```

In this approach, we create a `frequencyMap`, which is a HashMap that stores the frequencies of each element in the array. We iterate through the array and update the frequencies in the map using the `put()` method. Afterward, we iterate through the map entries to find the element with the highest frequency (`maxFrequency`) and return its key (`mode`).

## Conclusion

In this article, we explored two different approaches to finding the mode of elements in a sorted Java array. The linear scan approach involves iterating through the array and keeping track of the frequencies, while the HashMap approach uses a map to store the frequencies. Depending on the size of the array and the expected frequency distribution, one approach may be more efficient than the other.