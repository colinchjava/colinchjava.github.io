---
layout: post
title: "Updates to Sealed classes in Java 18"
description: " "
date: 2023-10-24
tags: [references]
comments: true
share: true
---

Java 18 introduces several enhancements to the concept of sealed classes, providing more flexibility and control over class hierarchies. Sealed classes, introduced in Java 15, restrict the inheritance of a class to a predefined set of subclasses, allowing developers to create more stable and maintainable code.

## Table of Contents
- [Introduction](#introduction)
- [Sealed Classes in Java 15](#sealed-classes-in-java-15)
- [Updates in Java 18](#updates-in-java-18)
- [Summary](#summary)

## Introduction <a name="introduction"></a>

Sealed classes are a mechanism in Java that define a specific set of subclasses which can inherit from a superclass. This helps in enforcing strong encapsulation and prevents the uncontrolled extension of classes by unneeded subclasses.

## Sealed Classes in Java 15 <a name="sealed-classes-in-java-15"></a>

In Java 15, sealed classes were introduced with the `sealed` keyword. If a class is declared as sealed, it is restricted to allow inheritance only from a limited set of subclasses. These subclasses must be explicitly declared using the `permits` keyword.

```java
public sealed class Shape permits Circle, Rectangle {
    // Class definition
}
```

The `Shape` class in the above example is sealed and permits only the `Circle` and `Rectangle` classes to inherit from it.

## Updates in Java 18 <a name="updates-in-java-18"></a>

Java 18 brings a few important updates to sealed classes, making them even more powerful:

### 1. Widening the Permitted Subclasses
In earlier versions, once a class was declared as sealed, all the subclasses needed to be explicitly listed using the `permits` keyword in the superclass. However, in Java 18, there is a provision to enlarge the set of permitted subclasses. A sealed class can now have additional permitted subclasses added later without modifying the original class definition.

```java
public sealed class Shape permits Circle, Rectangle { // Original definition
    // Class definition
}

public final class Square extends Shape { // Extends Shape without additional permits
    // Class definition
}

public non-sealed class Triangle extends Shape { // New permitted subclass
    // Class definition
}
```

In the updated example, the original sealed class `Shape` permits `Circle` and `Rectangle`. However, in Java 18, we can introduce a new permitted subclass `Triangle` without modifying the original class definition. Additionally, we can have a non-sealed subclass `Square` without any additional permits.

### 2. Permitted Subclass Nesting
Java 18 also introduces the ability to nest the permitted subclasses within the superclass. This allows for better organization and grouping of related subclasses.

```java
public sealed class Shape {
    // Class definition

    public abstract sealed class TwoDimensionalShape permits Circle, Rectangle {
        // Class definition
    }

    public abstract sealed class ThreeDimensionalShape permits Sphere, Cube {
        // Class definition
    }
}
```

In the updated example, the sealed class `Shape` contains nested sealed classes (`TwoDimensionalShape` and `ThreeDimensionalShape`) which have their own set of permitted subclasses. This nesting improves the overall structure and readability of the class hierarchy.

## Summary <a name="summary"></a>

With the updates introduced in Java 18, sealed classes become even more flexible and versatile. These enhancements allow modifications to the set of permitted subclasses without directly modifying the original class definition. Also, the nesting of permitted subclasses adds a new level of organization and clarity to the class hierarchy. These improvements contribute to creating more robust and maintainable codebases in Java. 

#references:
- [Java 15 Sealed Classes JEP](https://openjdk.java.net/jeps/360)
- [Java 18 release notes](https://openjdk.java.net/projects/jdk/18/release-notes)