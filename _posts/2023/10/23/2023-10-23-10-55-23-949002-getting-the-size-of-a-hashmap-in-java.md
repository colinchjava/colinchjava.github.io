---
layout: post
title: "Getting the size of a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, the `HashMap` class is widely used for storing key-value pairs. It is important to know the size of a `HashMap` at any given point, as it can help in analyzing and optimizing the performance of your code.

To get the size of a `HashMap`, you can use the `size()` method provided by the `HashMap` class. 

Here's an example of how to use the `size()` method to get the size of a `HashMap`:

```java
import java.util.HashMap;

public class Main {
  public static void main(String[] args) {
    HashMap<String, Integer> hashMap = new HashMap<>();
    hashMap.put("A", 1);
    hashMap.put("B", 2);
    hashMap.put("C", 3);

    int size = hashMap.size();
    System.out.println("Size of HashMap: " + size);
  }
}
```

In this example, we create a `HashMap` and add three key-value pairs to it. Then, we use the `size()` method to get the size of the `HashMap`. Finally, we print the size to the console.

Running the above code will output:

```
Size of HashMap: 3
```

The `size()` method returns an `int` value representing the number of key-value pairs present in the `HashMap`.

It is important to note that the `size()` method has a time complexity of O(1), meaning it takes constant time to retrieve the size, regardless of the number of elements in the `HashMap`.

By knowing the size of a `HashMap`, you can make informed decisions about your code and design efficient algorithms that rely on the size of the `HashMap`.

**#java #hashmap**