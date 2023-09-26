---
layout: post
title: "Polymorphism and abstraction in Java"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

Polymorphism and abstraction are important concepts in object-oriented programming (OOP), and they play a crucial role in Java. Understanding these concepts can help you write more efficient and maintainable code.

## Abstraction

Abstraction is the process of simplifying complex systems by breaking them down into smaller, more manageable parts. In Java, abstraction is achieved through abstract classes and interfaces.

**Abstract Classes**: An abstract class is a class that cannot be instantiated and is meant to be extended by other classes. It serves as a blueprint for creating objects. Abstract classes may contain abstract methods, which are methods without an implementation. These methods are meant to be overridden by the subclass.

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
```

**Interfaces**: An interface is a collection of abstract methods that define a contract for classes to implement. It defines a set of methods that a class must implement, but it does not provide any implementation details. An interface allows for multiple inheritance, as a class can implement multiple interfaces.

```java
public interface Drawable {
    void draw();
}

public class Square implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a square...");
    }
}
```

## Polymorphism

Polymorphism refers to the ability of a single entity to take on different forms. In Java, polymorphism is achieved through method overriding and method overloading.

**Method Overriding**: Method overriding allows a subclass to provide its own implementation of a method that is already defined in its superclass. The method in the subclass must have the same name, return type, and parameters as the method in the superclass.

```java
public class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks");
    }
}
```

**Method Overloading**: Method overloading allows multiple methods with the same name but different parameters to coexist in the same class. The compiler determines which method to call based on the method arguments.

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```

## Conclusion

Polymorphism and abstraction are powerful features of Java that enable code reusability, flexibility, and extensibility. Understanding how to use these concepts effectively will help you write cleaner and more maintainable code. #Java #OOP