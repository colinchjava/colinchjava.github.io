---
layout: post
title: "Java interfaces and abstract classes"
description: " "
date: 2023-09-27
tags: [programming]
comments: true
share: true
---

When working with Java, you will often come across interfaces and abstract classes. These are two important concepts in object-oriented programming that allow for code reusability, abstraction, and polymorphism. In this blog post, we will explore what interfaces and abstract classes are, and when to use them in your Java projects.

## Interfaces

An interface in Java is a way to define a contract that classes can implement. It defines a set of methods that must be implemented by the classes that implement the interface. Here's an example of an interface:

```java
public interface Drawable {
    void draw();
}
```

In the above example, the `Drawable` interface declares a single method `draw()`. Any class that implements this interface is required to provide an implementation for the `draw()` method. 

Interfaces are useful when you want to define a common behavior that multiple unrelated classes can share. For example, if you have different shapes like `Rectangle`, `Circle`, and `Triangle`, you can define a `Drawable` interface that requires all shapes to implement a `draw()` method.

To implement an interface, a class uses the `implements` keyword. Here's an example:

```java
public class Rectangle implements Drawable {
    @Override
    public void draw() {
        // Provide implementation for drawing a rectangle
    }
}
```

A class can implement multiple interfaces by separating them with commas. Interfaces allow for multiple inheritance, which means a class can inherit behavior from multiple interfaces.

## Abstract Classes

An abstract class in Java is a class that cannot be instantiated. It is meant to be extended by other classes. Abstract classes are useful when you want to define common attributes and methods that can be shared by multiple subclasses.

Here's an example of an abstract class:

```java
public abstract class Animal {
    protected String name;

    public Animal(String name) {
        this.name = name;
    }

    public abstract void makeSound();

    public void eat() {
        // Provide implementation for eating
    }
}
```

In the above example, the `Animal` class is declared as abstract because it contains an abstract method `makeSound()`. Abstract methods are declared without a body and must be implemented by the subclasses. The `eat()` method, on the other hand, has a default implementation.

To create a subclass of an abstract class, you use the `extends` keyword. Here's an example:

```java
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}
```

The `Dog` class extends the `Animal` class and provides an implementation for the `makeSound()` method. It can also make use of the `eat()` method inherited from the `Animal` class.

In summary, interfaces and abstract classes are powerful tools in Java that allow for code reuse and abstraction. Interfaces define a contract that classes can implement, while abstract classes provide a common base for subclasses. Understanding when and how to use interfaces and abstract classes can greatly improve the design and maintainability of your Java projects.

#java #programming