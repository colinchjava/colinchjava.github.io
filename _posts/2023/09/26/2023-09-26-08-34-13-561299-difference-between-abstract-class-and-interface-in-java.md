---
layout: post
title: "Difference between abstract class and interface in Java"
description: " "
date: 2023-09-26
tags: [Java, Programming]
comments: true
share: true
---

When working with Java, you may come across the need to define common behavior for a set of classes. This is where abstract classes and interfaces come into play. Both abstract classes and interfaces provide a way to define common structure and functionality, but they have some key differences. In this blog post, we will explore the differences between abstract classes and interfaces in Java.

## Abstract Class

An abstract class in Java is a class that cannot be instantiated. It serves as a base class for other classes and is used to define common attributes and methods that derived classes can inherit. 

Here are some important points to note about abstract classes:

1. An abstract class can have both abstract and non-abstract methods. Abstract methods are those that are declared without an implementation and need to be implemented by the derived classes.
2. If a class extends an abstract class, it must implement all the abstract methods declared in the abstract class, unless the subclass itself is abstract.
3. An abstract class can have instance variables and constructors.
4. Abstract classes can be used to provide common implementation details to the derived classes.

Here's an example of an abstract class in Java:

```java
public abstract class Animal {
    String name;

    public Animal(String name) {
        this.name = name;
    }

    public abstract void makeSound();

    public void sleep() {
        System.out.println("Animal is sleeping");
    }
}
```

## Interface

An interface in Java is a collection of abstract methods. It defines a contract that implementing classes must adhere to. Unlike abstract classes, interfaces cannot have instance variables or constructors. They provide a way to achieve multiple inheritances in Java, as a class can implement multiple interfaces.

Here are some important points to note about interfaces:

1. All methods in an interface are implicitly public and abstract. They do not have a method body.
2. A class implementing an interface must provide implementations for all the methods declared in the interface.
3. Multiple interfaces can be implemented by a single class.
4. Interfaces are used to define common behavior across unrelated classes.

Here's an example of an interface in Java:

```java
public interface Drawable {
    void draw();
    void resize(int width, int height);
}
```

## Conclusion

In summary, abstract classes and interfaces in Java provide a way to define common behavior, but with some key differences. Abstract classes can have both abstract and non-abstract methods, can define instance variables, and can provide common implementation details. Interfaces, on the other hand, can only have abstract methods, cannot have instance variables, and are used to define common behavior across unrelated classes.

Understanding the differences between abstract classes and interfaces will help you choose the appropriate approach based on your specific needs when designing a Java application.

#Java #Programming