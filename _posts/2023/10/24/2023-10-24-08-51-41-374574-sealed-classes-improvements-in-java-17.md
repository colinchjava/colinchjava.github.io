---
layout: post
title: "Sealed classes improvements in Java 17"
description: " "
date: 2023-10-24
tags: [tech, programming]
comments: true
share: true
---

Java 17, the latest release of the Java programming language, brings several improvements to sealed classes. Sealed classes were introduced in Java 15 as a way to restrict the inheritance hierarchy of a class or an interface. They allow you to explicitly specify which classes or interfaces can extend or implement them.

## 1. Non-Sealed Classes Extending Sealed Classes

Prior to Java 17, sealed classes could only be extended by sealed and non-sealed classes within the same module. With the introduction of `permits` keyword, non-sealed classes can now extend sealed classes even if they are in different modules.

```java
// In module A
sealed class Shape permits Circle, Rectangle, Square {
    // ...
}

// In module B
non-sealed class Circle extends Shape {
    // ...
}

// In module C
non-sealed class Triangle extends Shape {
    // ...
}

```

In the example above, the `Circle` and `Triangle` classes can now extend the sealed `Shape` class, even though they are in different modules. This allows for greater extensibility and facilitates the modular design of your application.

## 2. Interfaces Allowed as Sealed Types

In Java 17, interfaces can now be used as sealed types. This means that a sealed class can specify interfaces as the permitted subtypes. This allows for more flexible design patterns and composition.

```java
sealed interface Vehicle permits Car, Bike, Truck {
    // ...
}
```

In the example above, the `Vehicle` interface is sealed and permits the implementation of various subtypes such as `Car`, `Bike`, and `Truck`. This enables you to define a common set of behaviors for all implementors of the `Vehicle` interface.

## 3. Improved Error Reporting

Java 17 provides improved error reporting for sealed classes. If a subclass or an implementing class violates the sealed class contract, the compiler provides more detailed error messages, clearly identifying the issue. This makes debugging and troubleshooting sealed class violations much easier.

## Summary

Java 17 brings significant improvements to sealed classes. You can now have non-sealed classes extending sealed classes across different modules, interfaces as sealed types, and better error reporting for sealed class violations. These enhancements enhance the flexibility and maintainability of your Java codebase, enabling you to design more robust and modular applications.

For more information on sealed classes, refer to the official Java Documentation: [https://docs.oracle.com/en/java/javase/17/language/sealed-classes.html](https://docs.oracle.com/en/java/javase/17/language/sealed-classes.html)

#tech #programming