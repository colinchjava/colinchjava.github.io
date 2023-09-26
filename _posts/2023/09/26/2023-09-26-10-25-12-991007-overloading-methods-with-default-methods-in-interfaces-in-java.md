---
layout: post
title: "Overloading methods with default methods in interfaces in Java"
description: " "
date: 2023-09-26
tags: [Java, MethodsOverloading]
comments: true
share: true
---

In Java, interfaces provide a way to define a contract for classes to implement. Traditionally, interfaces only allowed abstract methods, i.e., methods without a default implementation. However, starting from Java 8, default methods were introduced to interfaces, allowing the addition of new methods without breaking implementation in existing classes. 

One interesting feature of Java interfaces with default methods is the ability to overload methods. Overloading refers to the process of defining multiple methods with the same name but different parameters. It provides flexibility in handling various input scenarios.

To overload methods in interfaces, follow these steps:

## Step 1: Define the Interface

```java
public interface OverloadInterface {
    default void print(String message) {
        System.out.println("Default: " + message);
    }

    default void print(int number) {
        System.out.println("Default: " + number);
    }
}
```

The `OverloadInterface` interface defines two default methods named `print` with different parameter types: `String` and `int`. 

## Step 2: Implement the Interface

```java
public class MyClass implements OverloadInterface {
    @Override
    public void print(String message) {
        System.out.println("Implemented: " + message);
    }
}
```

The `MyClass` class implements the `OverloadInterface` and overrides the `print` method that takes a `String` parameter. 

## Step 3: Test the Overloaded Methods

```java
public class Main {
    public static void main(String[] args) {
        MyClass myClass = new MyClass();
        
        // Overloaded method with String parameter
        myClass.print("Hello");

        // Overloaded method with int parameter
        myClass.print(123);
    }
}
```

In the `main` method, we create an instance of `MyClass` and invoke the overloaded `print` methods with different argument types.

## Conclusion

Overloading methods in interfaces with default methods in Java 8 and above allows interfaces to have multiple methods with the same name but different parameter types. This feature provides flexibility and enhances code reusability. By leveraging the power of default methods, interfaces in Java have become more powerful and versatile.

#Java #MethodsOverloading