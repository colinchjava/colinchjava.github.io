---
layout: post
title: "Updates to preview features in Java 22"
description: " "
date: 2023-10-24
tags: [PreviewUpdates]
comments: true
share: true
---

Java 22 is set to bring some exciting updates to its preview features. Preview features are language and VM features that are introduced in a specific Java version for experimental purposes. They are subject to change or removal in future Java versions based on user feedback and further development.

In this blog post, we will explore some of the updates and enhancements coming to the preview features in Java 22.

## Sealed Classes

Sealed classes were introduced as a preview feature in Java 15 and continue to evolve in Java 22. The updated version introduces a more flexible approach for declaring the permitted subclasses of a sealed class.

The `sealed` modifier is used to define a sealed class, and you can now use the `permits` clause to explicitly declare the permitted subclasses. This allows for better control over the subclasses that can be extended from a sealed class.

```java
public sealed class Shape permits Circle, Triangle, Rectangle {
    // Class body
}
```

## Pattern Matching for Switch

Pattern matching for `switch` is another preview feature that is getting updates in Java 22. This feature provides a concise way of writing `switch` statements by combining pattern matching with `switch` expressions.

With the new updates, you can utilize pattern variables in `switch` statements to capture the matched value and use it within the block. This eliminates the need to repeat the variable declaration and allows for more readable code.

```java
int statusCode = 200;

switch (statusCode) {
    case 200 -> {
        String message = "OK";
        // Do something with message
    }
    case 404 -> {
        String message = "Not Found";
        // Do something with message
    }
    default -> {
        String message = "Unknown";
        // Do something with message
    }
}
```

## Records

Records were introduced as a preview feature in Java 14, and Java 22 brings some enhancements to this concise class declaration feature. The update allows you to declare instance fields and provide a body for record classes.

By including an explicit field declaration, you can customize the field names and their data types within a record class. This provides more flexibility when working with records.

```java
record Person(String name, int age) {
    String occupation; // Additional field declaration
    // Class body
}
```

## JEPs to Follow

Java 22 is still in the early stages of development, and several Java Enhancement Proposals (JEPs) are targeted for inclusion in the final release. Some notable JEPs to watch out for are JEP 371 (Hidden Classes) and JEP 376 (ZGC: Concurrent Thread-Stack Processing).

Stay tuned for the official release of Java 22 to explore these exciting updates and enhancements to preview features.

[#Java22](https://www.java.com) [#PreviewUpdates](https://www.java.com/preview-updates)