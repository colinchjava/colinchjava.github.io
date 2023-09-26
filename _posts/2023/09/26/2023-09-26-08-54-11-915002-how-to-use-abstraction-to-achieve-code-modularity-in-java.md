---
layout: post
title: "How to use abstraction to achieve code modularity in Java"
description: " "
date: 2023-09-26
tags: [abstraction]
comments: true
share: true
---

In object-oriented programming, **abstraction** is an important concept that allows us to create modular and reusable code. It helps in managing complexity and making code more maintainable. Java, being an object-oriented language, provides powerful tools for implementing abstraction in our code.

## Understanding Abstraction

**Abstraction** is the process of hiding complex implementation details and exposing only the essential features or functionalities of an object. It allows us to represent real-world entities as abstract entities in our code.

In Java, abstraction is achieved through **interfaces** and **abstract classes**.

### Interfaces

An interface in Java is a contract or a blueprint that defines a set of abstract methods that a class must implement. It provides a common set of behaviors that multiple classes can adhere to.

```java
public interface Drawable {
    void draw();
}
```

Here, we have defined an interface called `Drawable` with a single abstract method `draw()`. Any class that implements this interface is required to provide an implementation for the `draw()` method.

### Abstract Classes

An abstract class is a class that cannot be instantiated but can be inherited by subclasses. It can contain both abstract and non-abstract methods. Abstract methods are declared without any implementation and must be overridden by the subclasses.

```java
public abstract class Shape {
    abstract void draw();
    
    void printInfo() {
        System.out.println("This is a shape.");
    }
}
```

In the above example, we have defined an abstract class called `Shape`. It contains an abstract method `draw()` and a non-abstract method `printInfo()`. The `draw()` method must be implemented by any class that extends the `Shape` class.

## Achieving Modularity with Abstraction

Now, let's see how abstraction helps us achieve code modularity in Java. By using interfaces and abstract classes, we can create independent modules that can be easily maintained and extended.

For example, consider a simple application that deals with different shapes. We can define an interface called `Drawable` to abstract the common feature of drawing:

```java
public interface Drawable {
    void draw();
}
```

Then, we can create different shape classes that implement this interface, such as `Circle` and `Rectangle`:

```java
public class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

public class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}
```

These shape classes can have their own specific implementations but still adhere to the common behavior defined by the `Drawable` interface.

In another part of our application, we can have a `Canvas` class that can draw any `Drawable` object:

```java
public class Canvas {
    public void drawShape(Drawable shape) {
        shape.draw();
    }
}
```

By using abstraction, we have achieved modularity in our code. The `Canvas` class is not tightly coupled with specific shape implementations; it can work with any object that implements the `Drawable` interface.

This modular design allows us to easily add new shape classes without modifying the `Canvas` class or any other parts of the codebase.

## Conclusion

Abstraction is a powerful technique in Java that allows us to create modular and reusable code. By using interfaces and abstract classes, we can abstract common behaviors, hide implementation details, and achieve code modularity. This makes our code more maintainable and extensible. #java #abstraction