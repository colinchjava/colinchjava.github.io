---
layout: post
title: "Implementing method overriding and dynamic polymorphism with Java objects"
description: " "
date: 2023-09-15
tags: [java, methodoverriding]
comments: true
share: true
---

Method overriding is a crucial concept in object-oriented programming that allows a subclass to provide its own implementation of a method defined in its superclass. This feature enables dynamic polymorphism, where the appropriate method is called based on the actual type of the object at runtime. In this blog post, we will explore how to implement method overriding and dynamic polymorphism using Java objects.

## Method Overriding
In Java, method overriding is achieved by redefining a method in a subclass with the same name, return type, and parameters as the method in the superclass. The `@Override` annotation is used to indicate that a method is intended to override a superclass method. Here's an example that demonstrates method overriding:

```java
class Animal {
    public void makeSound() {
        System.out.println("Animal makes sound");
    }
}

class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal();
        Cat cat = new Cat();
        
        animal.makeSound(); // Output: Animal makes sound
        cat.makeSound();    // Output: Meow
    }
}
```
In the example above, we define a superclass `Animal` with a `makeSound` method. The `Cat` class extends `Animal` and overrides the `makeSound` method to produce the sound of a cat. In the `main` method, we create an instance of `Animal` and `Cat` and invoke the `makeSound` method. As expected, the overridden method in the subclass is invoked, demonstrating method overriding.

## Dynamic Polymorphism
Dynamic polymorphism, also known as late binding or runtime polymorphism, allows us to treat objects of different classes as objects of a common superclass. The JVM determines the actual type of the object at runtime and invokes the appropriate overridden method. Here's an example that demonstrates dynamic polymorphism:

```java
class Vehicle {
    public void start() {
        System.out.println("Vehicle is starting");
    }
}

class Car extends Vehicle {
    @Override
    public void start() {
        System.out.println("Car is starting");
    }
}

class Truck extends Vehicle {
    @Override
    public void start() {
        System.out.println("Truck is starting");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle vehicle1 = new Vehicle();
        Vehicle vehicle2 = new Car();
        Vehicle vehicle3 = new Truck();
        
        vehicle1.start();  // Output: Vehicle is starting
        vehicle2.start();  // Output: Car is starting
        vehicle3.start();  // Output: Truck is starting
    }
}
```

In the example above, we have a superclass `Vehicle` and two subclasses `Car` and `Truck`. Each class overrides the `start` method with a specialized implementation. In the `main` method, we create instances of `Vehicle`, `Car`, and `Truck` and store them in variables of type `Vehicle`. When invoking the `start` method, the JVM determines the actual type of the object and calls the appropriate overridden method. This demonstrates dynamic polymorphism, as the behavior of the method differs based on the actual type of the object at runtime.

#java #methodoverriding #polymorphism