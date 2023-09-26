---
layout: post
title: "Constructor overloading with super keyword in Java"
description: " "
date: 2023-09-26
tags: [ConstructorOverloading]
comments: true
share: true
---

In object-oriented programming, **constructor overloading** is the ability to define multiple constructors with different parameter lists within a class. This allows objects to be initialized in different ways, providing flexibility and convenience to the programmer.

In Java, when a subclass is created, it automatically inherits the constructors of its superclass. However, if you want to **invoke a specific constructor of the superclass** from within the subclass constructor, you can use the `super` keyword.

## Using the `super` Keyword to Invoke Superclass Constructors

To invoke a superclass constructor, the `super` keyword is used along with parentheses, followed by the arguments required by the superclass constructor. This allows the subclass to pass arguments to the superclass constructor and initialize the inherited members.

Let's look at an example to understand constructor overloading with the `super` keyword in Java:

```java
public class Vehicle {
    private String brand;
    private int year;

    public Vehicle(String brand, int year) {
        this.brand = brand;
        this.year = year;
    }

    // Getters and setters

    // Other methods
}
```

```java
public class Car extends Vehicle {
    private String model;

    public Car(String brand, int year, String model) {
        super(brand, year); // Invokes the superclass constructor
        this.model = model;
    }

    // Getters and setters

    // Other methods
}
```

In the above example, we have a `Vehicle` class with a parameterized constructor that takes `brand` and `year` as arguments. The `Car` class extends the `Vehicle` class and has an additional property called `model`. In the `Car` class constructor, the `super(brand, year)` statement is used to invoke the superclass constructor and initialize the `brand` and `year` fields inherited from the `Vehicle` class.

## Benefits of Constructor Overloading with `super`

- **Code Reusability**: By using the `super` keyword to invoke the superclass constructor, we can reuse the initialization logic defined in the superclass.
- **Flexibility**: Constructor overloading allows us to create objects of the subclass in various ways, based on the arguments passed to the constructors.

By leveraging constructor overloading and the `super` keyword, we can efficiently initialize objects in Java, providing flexibility and code reusability in our applications.

#Java #ConstructorOverloading #SuperKeyword