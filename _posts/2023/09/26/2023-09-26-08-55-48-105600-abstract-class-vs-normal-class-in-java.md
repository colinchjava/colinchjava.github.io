---
layout: post
title: "Abstract class vs. normal class in Java"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

When designing object-oriented programs in Java, we often come across the decision of whether to use an abstract class or a normal class. Both options have their own advantages and use cases, so let's explore the differences between the two.

## Normal Class: ##
  
A normal class is a concrete implementation that can be instantiated to create objects. It defines complete functionality and behavior, and can be directly used to create objects.

**Advantages:**
- Can create multiple instances of the class.
- Provides a complete implementation of methods.

**Use Cases:**
- When we want to create objects with predefined behavior and complete implementation.
- When there is no need for other classes to inherit from it.

Example of a normal class in Java:

```java
public class Person {
    private String name;
    
    public Person(String name) {
        this.name = name;
    }
    
    public void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}
```

## Abstract Class: ##

An abstract class is a class that cannot be instantiated, serving as a blueprint for other classes to inherit from. It provides a partial implementation and defines common attributes and methods that other classes can reuse.

**Advantages:**
- Allows for code reusability and promotes consistency across different classes.
- Defines common methods that subclasses can implement or override.
- Can have both abstract and non-abstract methods.

**Use Cases:**
- When we want to provide common functionality to multiple related classes.
- When we want to enforce a specific structure and behavior across multiple subclasses.

Example of an abstract class in Java:

```java
public abstract class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public abstract void makeSound();
    
    public void eat() {
        System.out.println(name + " is eating.");
    }
}
```

## Conclusion: ##

In Java, choosing between an abstract class and a normal class depends on the specific requirements of your application. If you need a complete implementation with multiple instances, a normal class is suitable. On the other hand, if you want to provide common functionality and enforce a structure for subclasses, an abstract class is the way to go.

#Java #OOP