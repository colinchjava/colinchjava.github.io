---
layout: post
title: "Overloading methods in subclasses"
description: " "
date: 2023-09-26
tags: [programming]
comments: true
share: true
---

In object-oriented programming, **overloading** refers to defining multiple methods with the same name but different parameter types or parameter lists within a class. This allows you to perform different operations based on the varying parameters provided.

When it comes to subclassing, you can also overload methods inherited from a superclass. This means that you can have methods in the subclass with the same name as those in the superclass, but with different parameter types or lists.

Let's look at an example to understand how overloading methods in subclasses work:

```java
public class Shape {
    public void draw() {
        System.out.println("Drawing a shape");
    }
}

public class Circle extends Shape {
    public void draw() {
        System.out.println("Drawing a circle");
    }
    
    public void draw(int radius) {
        System.out.println("Drawing a circle with radius: " + radius);
    }
}

public class Main {
    public static void main(String[] args) {
        Shape shape = new Shape();
        shape.draw();
        
        Circle circle = new Circle();
        circle.draw();
        circle.draw(5);
    }
}
```

In the above example, we have a superclass `Shape` with a `draw()` method. The `Circle` class is a subclass of `Shape` and it overrides the `draw()` method to draw a circle, using the `draw()` method of the superclass.

Additionally, the `Circle` class also has an overloaded `draw()` method that takes an integer parameter representing the radius of the circle. This method is specific to the `Circle` class and is not present in the superclass.

When we create an instance of the `Circle` class and call the `draw()` method, it first invokes the overridden `draw()` method from the superclass, which prints "Drawing a circle". Then, if we call the `draw(int radius)` method with a parameter, it will invoke the overloaded method and print "Drawing a circle with radius: [radius]".

This allows us to have different versions of the `draw()` method based on the type and number of parameters, providing more flexibility and customization in the subclass.

By understanding and utilizing method overloading in subclasses, you can make your code more modular and adaptable to different use cases.

#programming #java