---
layout: post
title: "Abstract methods vs. static methods in interfaces in Java"
description: " "
date: 2023-09-26
tags: [Java, Interfaces]
comments: true
share: true
---

When working with interfaces in Java, we often come across two types of methods: abstract methods and static methods. Both serve different purposes and have their own set of rules and use cases. In this article, we will explore the key differences between abstract methods and static methods in interfaces.

## Abstract Methods in Interfaces

An abstract method in an interface is a method declaration without an implementation. It provides a contract for the classes that implement the interface to define the method's behavior. Abstract methods define what a class should do rather than how it should do it.

```java
public interface Drawable {
    void draw();
}
```

In the example above, the `Drawable` interface declares an abstract method `draw()` without any implementation. Any class that implements the `Drawable` interface must provide its own implementation of the `draw()` method.

## Static Methods in Interfaces

A static method in an interface is a method that belongs to the interface itself and not to any specific instance of the interface. Static methods can be called directly on the interface and do not require an instance to be created.

```java
public interface Logger {
    static void log(String message) {
        System.out.println("Logging: " + message);
    }
}
```

In the above example, the `Logger` interface defines a static method `log()` that can be called directly on the interface. No instance of the interface is needed to invoke this method.

## Key Differences

Now that we have seen examples of both abstract methods and static methods in interfaces, let's highlight their key differences:

1. **Implementation:** Abstract methods require classes that implement the interface to provide an implementation. Static methods, on the other hand, provide a default implementation that can be used directly without any additional implementation.

2. **Method Invocation:** Abstract methods are invoked on instances of the implementing class, while static methods are invoked directly on the interface itself.

3. **Inheritance:** Abstract methods can be inherited by subclasses, and they must be implemented. Static methods cannot be overridden or inherited.

## Conclusion

Abstract methods and static methods in interfaces serve different purposes. Abstract methods provide a contract for implementing classes to define their behavior, while static methods provide a default implementation that can be called directly on the interface itself. Understanding the differences between these two types of methods in interfaces is essential for writing clean and concise Java code.

#Java #Interfaces