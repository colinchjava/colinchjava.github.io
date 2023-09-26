---
layout: post
title: "Abstract class vs. interface in Java 8"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

When working with Java 8, you have the option to use either abstract classes or interfaces to define reusable components and enforce contracts. Both abstract classes and interfaces play a crucial role in object-oriented programming, but they differ in their approach and usage. In this blog post, we will explore the differences between abstract classes and interfaces in Java 8 and discuss when to use each one.

## Abstract Classes

An abstract class is a class that cannot be instantiated and serves as a blueprint for derived classes. It can contain both abstract and non-abstract methods, and it may also have member variables. Abstract methods are implicitly defined as `abstract` and do not have a method body. Any class that extends an abstract class must implement all of its abstract methods.

Using `abstract` keyword in a class declaration makes it an abstract class:

```java
public abstract class AbstractClass {
    // Abstract method
    public abstract void someMethod();

    // Non-abstract method
    public void anotherMethod() {
        // method implementation
    }
}
```

Abstract classes can have constructors, fields, and non-abstract methods, providing a level of implementation that interfaces lack. They are commonly used when you want to provide a common base implementation for multiple derived classes. However, Java does not support multiple inheritance, so a class can only extend a single abstract class.

## Interfaces

Interfaces, on the other hand, represent contracts and do not provide any implementation. They define a set of methods that a class implementing the interface must implement. Unlike abstract classes, interfaces cannot have non-abstract methods or member variables. All methods in an interface are implicitly defined as `public` and `abstract`. Java 8 introduced `default` methods in interfaces, allowing interfaces to provide method implementations.

Using `interface` keyword creates an interface:

```java
public interface Interface {
    // Abstract method
    void someMethod();

    // Default method
    default void anotherMethod() {
        // method implementation
    }
}
```

This example interface defines an abstract method `someMethod()` and a default method `anotherMethod()`. The default method provides a default implementation that can be used by classes implementing the interface, but it can also be overridden if desired.

Interfaces are useful when you want to define behaviors that multiple unrelated classes can implement. A class can implement multiple interfaces, effectively achieving a form of multiple inheritance.

## Conclusion

In summary, abstract classes provide a way to define a common base implementation for derived classes, while interfaces define contracts and behaviors that unrelated classes can implement. Abstract classes can have constructors, fields, and non-abstract methods, whereas interfaces cannot. Choosing between abstract classes and interfaces in Java 8 depends on the specific use case and the desired level of flexibility and code reuse.

#Java #OOP