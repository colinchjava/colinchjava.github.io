---
layout: post
title: "Overloading constructors in inheritance hierarchy"
description: " "
date: 2023-09-26
tags: [inheritance, constructors]
comments: true
share: true
---

In object-oriented programming, constructors are special methods used to initialize objects. Inheritance allows us to create a hierarchy of classes with varying levels of specificity. When working with inheritance, it is often necessary to define multiple constructors with different parameters for each class in the hierarchy.

## What is constructor overloading?

Constructor overloading refers to the ability to define multiple constructors within a class, each with a different set of parameters. This allows objects to be initialized in different ways, depending on the parameters provided.

## Overloading constructors in an inheritance hierarchy

To overload constructors in an inheritance hierarchy, each subclass can have its own set of constructors, including those inherited from its parent class. This allows each subclass to define its specific initialization logic, while leveraging the constructors of its parent class.

Consider the following example, where we have a parent class `Vehicle` and two subclasses `Car` and `Motorcycle`. Each class has its own set of constructor overloads.

```java
public class Vehicle {
    private int numberOfWheels;

    public Vehicle(int numberOfWheels) {
        this.numberOfWheels = numberOfWheels;
    }

    // Other methods and fields...

}

public class Car extends Vehicle {
    private String brand;

    public Car(int numberOfWheels, String brand) {
        super(numberOfWheels);
        this.brand = brand;
    }

    // Other methods and fields...

}

public class Motorcycle extends Vehicle {
    private boolean hasSidecar;

    public Motorcycle(int numberOfWheels, boolean hasSidecar) {
        super(numberOfWheels);
        this.hasSidecar = hasSidecar;
    }

    // Other methods and fields...

}
```

In this example, the `Vehicle` class has a constructor that takes the `numberOfWheels` parameter. The `Car` subclass adds one more parameter `brand` to its constructor, while the `Motorcycle` subclass adds a `hasSidecar` parameter. Both subclasses invoke the superclass constructor using the `super` keyword.

This allows us to initialize objects of the `Car` and `Motorcycle` classes using different sets of parameters. For example:

```java
Car myCar = new Car(4, "Toyota");
Motorcycle myMotorcycle = new Motorcycle(2, true);
```

## Conclusion

Overloading constructors in an inheritance hierarchy is a powerful feature of object-oriented programming. It allows each subclass to define its initialization logic while leveraging the constructors of its parent class. By providing different ways to initialize objects, constructor overloading enables flexibility and reusability within a class hierarchy.

#inheritance #constructors