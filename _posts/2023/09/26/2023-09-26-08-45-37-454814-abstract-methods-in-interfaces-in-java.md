---
layout: post
title: "Abstract methods in interfaces in Java"
description: " "
date: 2023-09-26
tags: [Interfaces]
comments: true
share: true
---

Java interfaces are used to define a contract that classes must adhere to. Prior to Java 8, interfaces in Java could only contain method signatures, but no implementation. However, with the introduction of Java 8, it became possible to have default and static methods in interfaces, allowing for the inclusion of some implementation code.

Even though the inclusion of default and static methods was a significant addition, there was still a limitation in Java interfaces - the absence of abstract methods. Abstract methods are typically used in abstract classes to provide a common method signature that subclasses must implement. This limitation made it difficult to enforce requirements for certain methods to be implemented across multiple classes using interfaces.

## Java 8 onwards: Default Methods

Java 8 introduced the concept of default methods in interfaces, which provide a default implementation for a method. This means that now interfaces can provide method implementations, reducing the burden of implementing the same method across multiple classes.

To define a default method in an interface, use the `default` keyword followed by the method signature and implementation. The default method is automatically available to all classes implementing the interface, and it can be overridden by a class if desired. Here's an example:

```java
public interface Animal {
    void makeSound();
    
    default void sleep() {
        System.out.println("Zzzz...");
    }
}
```

In the above example, the `Animal` interface contains a default method `sleep()`. Any class implementing the `Animal` interface will have the `makeSound()` method to be implemented and the `sleep()` method available with a default implementation.

## Java 9 onwards: Private Methods

Java 9 introduced the concept of private methods in interfaces, which allows interfaces to include private methods to be used for internal implementation. Private methods in interfaces enhance code reusability and improve the readability of interface implementations.

To define a private method in an interface, use the `private` modifier before the method signature. Here's an example:

```java
public interface Vehicle {
    void start();
    
    default void stop() {
        // Some common code
        shutdownEngine();
    }
    
    private void shutdownEngine() {
        System.out.println("Shutting down engine...");
    }
}
```

In the above example, the `Vehicle` interface contains a private method `shutdownEngine()`. This method can only be accessed and used within the interface itself and cannot be accessed by any implementing class or outside the interface.

## Conclusion

Although Java interfaces couldn't originally include abstract methods, the introduction of default methods in Java 8 and private methods in Java 9 provided new ways to provide method implementations in interfaces. These additions have improved code reusability and made interfaces more versatile. It's important to understand how to use default and private methods effectively to design more robust and maintainable code. #Java #Interfaces