---
layout: post
title: "Differences between method overloading and method hiding in Java"
description: " "
date: 2023-09-26
tags: [Methods]
comments: true
share: true
---

In object-oriented programming, method overloading and method hiding are two important concepts used to handle functions with the same name but different parameters. While they may seem similar at first, there are significant differences between the two in Java. Let's explore these differences in detail.

## Method Overloading

Method overloading allows the same function name to be used with different parameters. In Java, overloaded methods must have the same name but must have a different number of parameters, order of parameters, or parameter types. This is also known as static polymorphism or compile-time polymorphism.

### Example:

```java
class MathUtils {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```

In the above example, the `add` method is overloaded with different parameter types (`int` and `double`). The compiler determines which overloaded method to call based on the arguments passed during the method call.

## Method Hiding

Method hiding, also known as static method binding, occurs when a subclass defines a static method with the same name and signature as a static method in its superclass. In Java, method hiding is determined at compile-time, as opposed to method overriding, which is determined at runtime.

### Example:

```java
class Vehicle {
    public static void showInfo() {
        System.out.println("I am a vehicle.");
    }
}

class Car extends Vehicle {
    public static void showInfo() {
        System.out.println("I am a car.");
    }
}
```

In the above example, the `showInfo` method is hidden in the `Car` class by defining another method with the same name and signature. When calling `showInfo` on an instance of `Car`, the method defined in the `Car` class will be invoked, even if the reference type is `Vehicle`.

## Key Differences

1. Method overloading is determined at compile-time based on the method signature, whereas method hiding is determined at compile-time based on the reference type.
2. Method overloading is used to create multiple methods with the same name but different parameter lists, allowing polymorphic behavior. Method hiding, on the other hand, is used to provide an alternative implementation of a static method in a subclass, without breaking the parent-child relationship.

Overall, method overloading and method hiding are fundamentally different concepts in Java. Method overloading allows multiple methods with the same name but different parameters, while method hiding involves creating a new method with the same name and signature in the subclass to hide the superclass method.

#Java #Methods