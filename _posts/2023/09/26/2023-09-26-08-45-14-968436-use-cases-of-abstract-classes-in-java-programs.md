---
layout: post
title: "Use cases of abstract classes in Java programs"
description: " "
date: 2023-09-26
tags: [AbstractClasses]
comments: true
share: true
---

In object-oriented programming, an abstract class is a class that cannot be instantiated, meaning you cannot create objects of an abstract class directly. However, abstract classes can be extended by other classes, and they serve as a blueprint for those classes to inherit from.

Here are some common use cases of abstract classes in Java programs:

## 1. Creating a Base Class

Abstract classes are often used to create a base class that provides a common interface and functionality for its subclasses. For example, consider a `Shape` class that defines common properties and methods for various types of shapes, such as `Circle` and `Rectangle`. The `Shape` class can be declared as an abstract class with abstract methods like `calculateArea()`. The subclasses (`Circle` and `Rectangle`) can then provide their own implementations of these methods based on their unique requirements.

```java
public abstract class Shape {
    // Abstract method to calculate the area
    public abstract double calculateArea();
    
    // Common method to display shape information
    public void displayInformation() {
        System.out.println("This is a shape.");
    }
}

public class Circle extends Shape {
    private double radius;
    
    // Implementing the abstract method to calculate the area
    @Override
    public double calculateArea() {
        return Math.PI * Math.pow(radius, 2);
    }
}

public class Rectangle extends Shape {
    private double length;
    private double width;
    
    // Implementing the abstract method to calculate the area
    @Override
    public double calculateArea() {
        return length * width;
    }
}
```

## 2. Providing Default Implementations

Abstract classes can also provide default implementations for certain methods, which can be inherited by the subclasses. This helps to reduce code duplication and provides a consistent behavior across the hierarchy. Subclasses can then choose to either use the default implementation or override it with their own implementation.

```java
public abstract class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    // Abstract method to make sound
    public abstract void makeSound();
    
    // Default implementation of eating behavior
    public void eat() {
        System.out.println(name + " is eating.");
    }
}

public class Dog extends Animal {
    public Dog (String name) {
        super(name);
    }
    
    // Implementing the abstract method to make sound
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

public class Cat extends Animal {
    public Cat (String name) {
        super(name);
    }
    
    // Implementing the abstract method to make sound
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}
```

In this example, the `Animal` class provides a default implementation of the `eat()` method, which is inherited by the subclasses `Dog` and `Cat`. The subclasses, however, override the abstract method `makeSound()` to provide the specific sound each animal makes.

Abstract classes are powerful tools in Java programming as they enable code abstraction, inheritance, and provide a way to define common behavior across a hierarchy of classes. By using abstract classes, you can design programs that are more flexible, maintainable, and extensible.

#Java #AbstractClasses