---
layout: post
title: "Checking if a HashMap is empty in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Here's a code example demonstrating how to check if a HashMap is empty:

```java
import java.util.HashMap;

public class EmptyHashMapExample {
    public static void main(String[] args) {
        HashMap<String, Integer> hashMap = new HashMap<>();

        // Adding key-value pairs to the HashMap
        hashMap.put("apple", 1);
        hashMap.put("banana", 2);
        hashMap.put("orange", 3);

        // Checking if the HashMap is empty
        boolean isEmpty = hashMap.isEmpty();

        // Displaying the result
        if (isEmpty) {
            System.out.println("HashMap is empty");
        } else {
            System.out.println("HashMap is not empty");
        }
    }
}
```

In this example, we create a new HashMap and add some key-value pairs to it. We then use the `isEmpty()` method to check if the HashMap is empty or not. The result is stored in the `isEmpty` variable, and we display the appropriate message based on the result.

Remember to import the `HashMap` class from the `java.util` package before using it.

You can find more information about the `isEmpty()` method in the [Java HashMap documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html#isEmpty()).