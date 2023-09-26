---
layout: post
title: "Abstract classes in Java inheritance hierarchy"
description: " "
date: 2023-09-26
tags: [Inheritance]
comments: true
share: true
---

In Java, abstract classes play an important role in the inheritance hierarchy. They serve as a base or template class from which other classes can inherit properties and methods. Abstract classes cannot be instantiated, meaning you cannot create objects directly from them. They are designed to be inherited by other classes, which can then provide concrete implementations for the abstract methods defined in the abstract class.

## Definition and Purpose

An abstract class in Java is identified by the `abstract` keyword. It is declared using the `abstract` modifier in the class definition. Abstract classes can contain both abstract and non-abstract methods. 

Abstract methods, marked with the `abstract` keyword, do not have any implementation in the abstract class. They only define the method signature, including the return type, name, and parameters. Concrete implementations of these methods must be provided by the subclasses that inherit from the abstract class.

The purpose of abstract classes is to define a common interface and behavior that can be shared among multiple related subclasses. This allows for code reuse and a more organized class hierarchy.

## Example  Code

```java
public abstract class Shape {
    public abstract double calculateArea();
    public abstract double calculatePerimeter();

    public void printDetails() {
        System.out.println("Shape: " + this.getClass().getSimpleName());
        System.out.println("Area: " + calculateArea());
        System.out.println("Perimeter: " + calculatePerimeter());
    }
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

    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

public class Square extends Shape {
    private double sideLength;

    public Square(double sideLength) {
        this.sideLength = sideLength;
    }

    @Override
    public double calculateArea() {
        return sideLength * sideLength;
    }

    @Override
    public double calculatePerimeter() {
        return 4 * sideLength;
    }
}
```

## Implementation and Inheritance

To create a class that inherits from an abstract class, the subclass must extend the abstract class using the `extends` keyword. The subclass is then responsible for implementing all the abstract methods declared in the abstract class.

In the example code, the `Circle` and `Square` classes inherit from the abstract class `Shape`. They provide concrete implementations for the `calculateArea()` and `calculatePerimeter()` methods. The `printDetails()` method is inherited from the abstract class and can be used for any subclass object.

## Conclusion

Abstract classes in Java allow for the creation of an inheritance hierarchy, providing a common interface and behavior among related subclasses. They define abstract methods that must be implemented by subclasses and can also include non-abstract methods with concrete implementations. Understanding the concept of abstract classes is crucial for building flexible and modular Java applications.

#Java #Inheritance