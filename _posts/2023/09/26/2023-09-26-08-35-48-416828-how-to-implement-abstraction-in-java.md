---
layout: post
title: "How to implement abstraction in Java"
description: " "
date: 2023-09-26
tags: [Java, Abstraction]
comments: true
share: true
---

Abstraction is an important concept in object-oriented programming that allows you to create classes with abstract methods and abstract classes. It helps you build a level of abstraction by hiding the implementation details and highlighting only the essential features of an object. In Java, abstraction is achieved using abstract classes and interfaces. In this article, we will explore how to implement abstraction in Java.

## Abstract Classes

An abstract class in Java is a class that cannot be instantiated, meaning you cannot create objects of an abstract class. It is used as a base class for other classes and can contain both abstract and non-abstract methods. To create an abstract class, use the `abstract` keyword before the class definition.

```java
public abstract class Animal {
    public abstract void sound();
    public void sleep() {
        System.out.println("Zzzz...");
    }
}
```

In the example above, we have an abstract class called `Animal` that has an abstract method `sound()` and a non-abstract method `sleep()`. Notice that the abstract method has no implementation, it is only declared. Abstract methods don't have a body and must be implemented by the subclass.

To use the `Animal` class, you need to create a subclass that extends it and provides an implementation for the abstract method.

```java
public class Dog extends Animal {
    public void sound() {
        System.out.println("Woof!");
    }
}
```

The `Dog` class extends the `Animal` class and overrides the `sound()` method with its specific implementation.

## Interfaces

An interface in Java is a collection of abstract methods. Like abstract classes, interfaces cannot be instantiated, and they can be implemented by multiple classes. To create an interface, use the `interface` keyword.

```java
public interface Shape {
    void draw();
    double getArea();
}
```

In the example above, we have an interface called `Shape` with two abstract methods: `draw()` and `getArea()`. By default, all methods in an interface are implicitly abstract and public.

To implement an interface in a class, use the `implements` keyword.

```java
public class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public void draw() {
        System.out.println("Drawing a circle");
    }

    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

The `Circle` class implements the `Shape` interface and provides implementations for the `draw()` and `getArea()` methods.

## Conclusion

Implementing abstraction in Java using abstract classes and interfaces is a powerful way to create modular and extensible code. Abstract classes allow you to define common properties and behaviors in a base class, while interfaces enable you to define a contract that classes must adhere to. By leveraging abstraction, you can build flexible and scalable software systems. So go ahead and start using abstraction in your Java projects to take advantage of its benefits.

#Java #Abstraction