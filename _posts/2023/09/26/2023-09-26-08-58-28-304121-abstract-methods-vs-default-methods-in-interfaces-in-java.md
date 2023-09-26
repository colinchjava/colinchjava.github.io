---
layout: post
title: "Abstract methods vs. default methods in interfaces in Java"
description: " "
date: 2023-09-26
tags: [InterfaceMethods]
comments: true
share: true
---

Interfaces in Java provide a way to define contracts that classes can implement. They typically contain abstract methods, which are by default public and must be implemented by the classes that implement the interface. However, starting from Java 8, interfaces can also contain default methods. Let's explore the differences between abstract methods and default methods in interfaces.

## Abstract Methods

Abstract methods in interfaces are declarations without an implementation. They are typically used to define a set of operation signatures that implementing classes must provide. Here's an example of an interface with an abstract method:

```java
public interface Drawable {
    void draw();
}
```

In the above code, `draw()` is an abstract method in the `Drawable` interface. Any class that implements this interface must provide an implementation for the `draw()` method.

## Default Methods

Default methods were introduced in Java 8 and provide a way to add methods with a default implementation in interfaces. These methods have an actual implementation in the interface itself, which can be used by all implementing classes. Here's an example:

```java
public interface Drawable {
    void draw();
    
    default void resize() {
        System.out.println("Resizing the drawable object.");
    }
}
```

In the code snippet above, `resize()` is a default method added to the `Drawable` interface. Unlike abstract methods, classes that implement this interface are not required to provide an implementation for default methods. Implementing classes can choose to override the default method if needed.

## Key Differences

### Role and Usage

- Abstract methods: They define methods that must be implemented by the implementing classes. These methods represent a contract that must be fulfilled.
- Default methods: They provide a default implementation that can be used by all implementing classes. They offer a convenient way to add new behavior to an interface without breaking existing implementations.

### Inheritance

- Abstract methods: When a class implements an abstract method from an interface, it is required to provide an implementation.
- Default methods: Implementing classes can choose not to override a default method. In such cases, the default implementation from the interface will be used.

### Multiple Inheritance

- Abstract methods: Interfaces can have multiple abstract methods, which can be implemented by a single class.
- Default methods: A class implementing multiple interfaces having the same default method could lead to a conflict. In such cases, the implementing class must explicitly override the default method.

## Conclusion

Abstract methods and default methods in interfaces serve different purposes. Abstract methods define a contract that must be fulfilled by implementing classes, while default methods provide a default implementation that can be used by all implementing classes. Understanding their differences is crucial when designing and implementing interfaces in Java.

#Java #InterfaceMethods