---
layout: post
title: "Using enums as values in a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, enums are a powerful way to define a set of constant values. They can be used in various scenarios to represent a finite set of values. HashMap is a widely used data structure in Java that allows us to map keys to values. While it is common to use primitive data types or objects as values in a HashMap, it is also possible to use enums as values.

## Creating an Enum

Let's start by creating an enum that represents different car brands:

```java
public enum CarBrand {
    TOYOTA,
    HONDA,
    BMW,
    MERCEDES,
    FORD
}
```

Here, we have defined a CarBrand enum with five possible values.

## Using Enums as Values in HashMap

To use enums as values in a HashMap, you need to declare the HashMap with the enum type as the value type. Here's an example of how you can create a HashMap using CarBrand enum as the value:

```java
import java.util.HashMap;

public class EnumHashMapExample {
    public static void main(String[] args) {
        HashMap<String, CarBrand> carMap = new HashMap<>();
        
        carMap.put("Camry", CarBrand.TOYOTA);
        carMap.put("Accord", CarBrand.HONDA);
        carMap.put("3 Series", CarBrand.BMW);
        carMap.put("C-Class", CarBrand.MERCEDES);
        carMap.put("F-150", CarBrand.FORD);
        
        System.out.println(carMap.get("Camry")); // Output: TOYOTA
    }
}
```

In the above example, we created a HashMap called `carMap` with the key as a `String` type and the value as a `CarBrand` enum. We then added entries to the map using the `put` method.

You can access the value associated with a key using the `get` method, just like we did in the last line of the example.

## Benefits of Using Enums as Values in HashMap

Using enums as values in a HashMap can be beneficial in various scenarios:

1. Type safety: Enums provide type safety as they restrict the possible values to the ones defined in the enum itself. This helps to avoid accidental assignments of incorrect values.
2. Readability: Using enums as values can enhance code readability by providing meaningful names to the constants.
3. Easy comparison: Enums can be compared directly using the `==` operator, making comparisons in the HashMap straightforward.

Enums offer a great way to define a fixed set of values that can be used as values in a HashMap. By using enums, you can ensure type safety and improve code readability.

# Conclusion

In this blog post, we learned how to use enums as values in a HashMap in Java. We discussed how to create an enum, initialize a HashMap with the enum type as the value, and access the values stored in the HashMap. We also highlighted the benefits of using enums as values in a HashMap.