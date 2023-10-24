---
layout: post
title: "Functional interfaces in Java 8"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Java 8, the concept of functional programming was introduced with the addition of lambda expressions and functional interfaces. Functional interfaces are interfaces that only have one abstract method and are used to represent lambdas or method references.

## Creating a Functional Interface

To create a functional interface, you simply need to declare an interface with one abstract method. For example:

```java
@FunctionalInterface
public interface MyFunctionalInterface {
    void doSomething();
}
```

The `@FunctionalInterface` annotation is used to indicate that an interface is intended to be functional.

## Using a Functional Interface

Once you have defined a functional interface, you can use lambdas or method references to implement its abstract method.

### Lambda Expressions

A lambda expression is a concise way of expressing a method implementation. It is represented by the arrow `->` and consists of parameters, an arrow, and a body. For example:

```java
MyFunctionalInterface myFunction = () -> {
    // implementation of doSomething method
    System.out.println("Doing something");
};
```

### Method References

Method references allow you to reference an existing method as the implementation of a functional interface. There are four types of method references: static method references, instance method references, constructor references, and arbitrary object method references.

```java
// Static Method Reference
MyFunctionalInterface myFunction = ClassName::staticMethodName;

// Instance Method Reference
MyClass myObject = new MyClass();
MyFunctionalInterface myFunction = myObject::instanceMethodName;

// Constructor Reference
MyFunctionalInterface myFunction = ClassName::new;

// Arbitrary Object Method Reference
MyClass myObject = new MyClass();
MyFunctionalInterface myFunction = myObject::instanceMethodName;
```

## Built-in Functional Interfaces

Java 8 provides several built-in functional interfaces in the `java.util.function` package, which are commonly used in functional programming. Some of the frequently used ones are:

- `Supplier`: represents a supplier of results.
- `Consumer`: represents an operation that consumes a single input argument and returns no result.
- `Function`: represents a function that takes one argument and produces a result.
- `Predicate`: represents a predicate (boolean-valued function) of one argument.

These functional interfaces come with their own set of methods for different purposes.

## Conclusion

Functional interfaces in Java 8 enable the use of lambda expressions and method references, making the code more concise and expressive. They provide a way to represent behaviors as objects and support functional programming paradigms. Functional interfaces, along with built-in functional interfaces, play a crucial role in writing more functional and modular code in Java.

---
References:
- [Oracle Java Documentation - Functional Interfaces](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)
- [Baeldung - Guide to Java 8 Functional Interfaces](https://www.baeldung.com/java-8-functional-interfaces)