---
layout: post
title: "Abstract methods vs. concrete methods in Java"
description: " "
date: 2023-09-26
tags: [Java, AbstractMethods]
comments: true
share: true
---

In Java, there are two types of methods: abstract methods and concrete methods. Understanding the difference between these two types is fundamental for designing and implementing classes effectively. Let's take a closer look at what abstract and concrete methods are and how they are used in Java.

## Abstract Methods

An **abstract method** is a method that is declared without an implementation. It provides a blueprint for subclasses to follow, defining the signature (name, parameters, and return type) that the subclass must implement. Abstract methods are declared using the `abstract` keyword and do not have a body.

Here is an example of an abstract method in Java:

```java
public abstract class Shape {
    public abstract double calculateArea();
}
```

In the above code snippet, the `Shape` class declares an abstract method `calculateArea()`. Any class that extends the `Shape` class must provide an implementation for the `calculateArea()` method.

## Concrete Methods

A **concrete method** is a method that has an implementation and provides the actual behavior of the method. Unlike abstract methods, concrete methods have a body and can be directly executed.

Here is an example of a concrete method in Java:

```java
public class Square extends Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    @Override
    public double calculateArea() {
        return side * side;
    }
}
```

In this example, the `Square` class extends the `Shape` class and provides an implementation for the `calculateArea()` method. The `calculateArea()` method in the `Square` class returns the area of a square based on its side length.

## Key Differences and Usage

The key differences between abstract methods and concrete methods are:

- Abstract methods are declared without an implementation, while concrete methods have a body.
- Abstract methods are used to provide a contract for subclasses to implement, while concrete methods provide the actual behavior.

Abstract methods are typically used in abstract classes or interfaces to define a common behavior that must be implemented by subclasses. Concrete methods, on the other hand, provide specific behavior and can be directly executed.

## Conclusion

Understanding the difference between abstract methods and concrete methods is crucial for writing effective Java code. Abstract methods serve as blueprints for subclasses to follow, while concrete methods provide the actual behavior. By utilizing these two types of methods correctly, you can design well-structured and maintainable Java classes and interfaces.

#Java #AbstractMethods #ConcreteMethods