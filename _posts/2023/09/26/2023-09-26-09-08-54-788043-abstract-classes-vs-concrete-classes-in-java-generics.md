---
layout: post
title: "Abstract classes vs. concrete classes in Java generics"
description: " "
date: 2023-09-26
tags: [summary, javagenerics]
comments: true
share: true
---

When working with Java generics, it is important to understand the difference between abstract classes and concrete classes. Both types of classes can be used as type parameters in generics, but they have distinct characteristics and use cases.

## Abstract Classes

Abstract classes are used to define common behavior and characteristics that can be inherited by multiple subclasses. They cannot be instantiated directly, but they can be extended by other classes. Abstract classes can have both abstract methods (which are defined without an implementation) and concrete methods (which have an implementation).

When using abstract classes as type parameters in generics, it provides flexibility. You can specify that the generic type parameter must be a subclass of the abstract class, allowing you to work with a range of related classes.

Here is an example:

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        // implementation for drawing a circle
    }
}

class Triangle extends Shape {
    void draw() {
        // implementation for drawing a triangle
    }
}

class Drawing<T extends Shape> {
    T shape;

    Drawing(T shape) {
        this.shape = shape;
    }

    void drawShape() {
        shape.draw();
    }
}

public class Main {
    public static void main(String[] args) {
        Drawing<Circle> circleDrawing = new Drawing<>(new Circle());
        circleDrawing.drawShape();

        Drawing<Triangle> triangleDrawing = new Drawing<>(new Triangle());
        triangleDrawing.drawShape();
    }
}
```

In the above example, the `Drawing` class is a generic class that takes a type parameter `T` which must be a subclass of the `Shape` abstract class. This allows us to create different instances of `Drawing` with different shapes (circle or triangle).

## Concrete Classes

Concrete classes, on the other hand, can be instantiated directly and used as type parameters in generics. They provide specific implementations for methods and can be used to create objects directly.

Here is an example:

```java
class Box<T> {
    private T content;

    public Box(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>("Hello");
        String content = stringBox.getContent();
        System.out.println(content);

        Box<Integer> integerBox = new Box<>(42);
        int number = integerBox.getContent();
        System.out.println(number);
    }
}
```

In the above example, we have a generic class `Box` that can hold any type of object. We can create instances of `Box` using concrete classes as type parameters (e.g., `Box<String>` or `Box<Integer>`). This allows us to have type safety while being able to store and retrieve different types of objects.

#summary #javagenerics