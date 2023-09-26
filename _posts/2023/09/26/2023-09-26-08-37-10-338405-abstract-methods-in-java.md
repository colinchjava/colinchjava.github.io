---
layout: post
title: "Abstract methods in Java"
description: " "
date: 2023-09-26
tags: [Java, AbstractMethods]
comments: true
share: true
---

Java is an object-oriented programming language that allows you to define abstract methods in order to enforce a certain behavior in classes that inherit from a parent class. Abstract methods provide a way to declare a method without providing an implementation. This means that subclasses are required to implement the abstract method when extending the parent class.

## What is an abstract method?

An abstract method is a method declaration without a body, denoted by the `abstract` modifier. It exists only in an abstract class or interface and serves as a "contract" for the subclasses to fulfill. The purpose of an abstract method is to define a common behavior that all subclasses must have, but the actual implementation may vary depending on the specific requirements of each subclass.

## Syntax of an abstract method

To define an abstract method in Java, you need to follow a specific syntax:

```java
public abstract returnType methodName(parameters);
```

- `public`: It is the access modifier, indicating that the method can be accessed from anywhere.
- `abstract`: It is the keyword that defines the method as abstract, indicating that it does not have a body or implementation.
- `returnType`: It represents the data type of the value returned by the method.
- `methodName`: It is the name of the abstract method.
- `parameters`: They are the input parameters required by the method (if any).

## Example of using abstract methods

Let's consider an example where we have an abstract class `Shape` with an abstract method `calculateArea()`. We'll create two subclasses, `Circle` and `Rectangle`, that inherit from the `Shape` class and implement the `calculateArea()` method according to their specific shape formulas.

```java
public abstract class Shape {
    public abstract double calculateArea();
}

public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

public class Rectangle extends Shape {
    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }
}
```

In the above example, the `Shape` class defines the abstract method `calculateArea()`. The `Circle` and `Rectangle` classes extend the `Shape` class and provide their own implementation of the `calculateArea()` method.

## Conclusion

Abstract methods in Java allow you to define a contract or common behavior that all subclasses must adhere to. By using abstract methods, you can enforce a specific behavior in subclasses while allowing each subclass to provide its own implementation. Abstract methods are a powerful tool in object-oriented programming, enabling code reusability and extensibility.

#Java #AbstractMethods