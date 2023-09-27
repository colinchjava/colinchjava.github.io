---
layout: post
title: "Object-oriented programming in Java"
description: " "
date: 2023-09-27
tags: [Java]
comments: true
share: true
---

## Introduction to Object-Oriented Programming

Object-oriented programming (OOP) is a programming paradigm that focuses on creating modular and reusable code using objects. It is based on the concept of "objects," which encapsulate data and the operations that can be performed on that data.

Java is a popular programming language that fully supports object-oriented programming. It provides features such as classes, objects, inheritance, polymorphism, and encapsulation, making it a powerful tool for building robust and scalable applications.

## Classes and Objects in Java

In Java, a class is a blueprint for creating objects. It defines the properties (data) and behavior (methods) that objects of that class can have. To create an object in Java, you need to instantiate a class using the `new` keyword.

```java
public class Car {
    String color;
    int numberOfDoors;

    public void start() {
        System.out.println("Car started!");
    }

    public void accelerate() {
        System.out.println("Car accelerated!");
    }

    public void stop() {
        System.out.println("Car stopped!");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car(); // Creating an object of the Car class
        myCar.color = "Red";
        myCar.numberOfDoors = 4;

        myCar.start(); // Calling the start() method
        myCar.accelerate(); // Calling the accelerate() method
        myCar.stop(); // Calling the stop() method
    }
}
```

In the above example, we have a `Car` class with two properties (`color` and `numberOfDoors`) and three methods (`start()`, `accelerate()`, and `stop()`). We create an object `myCar` of the `Car` class and set its properties. We then call the methods on the object to perform various operations.

## Inheritance and Polymorphism in Java

Inheritance is an essential concept in OOP that allows the creation of new classes based on existing classes. In Java, you can use the `extends` keyword to create a subclass that inherits properties and methods from a superclass.

```java
public class Vehicle {
    String color;

    public void start() {
        System.out.println("Vehicle started!");
    }

    public void stop() {
        System.out.println("Vehicle stopped!");
    }
}

public class Car extends Vehicle {
    int numberOfDoors;

    public void accelerate() {
        System.out.println("Car accelerated!");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.color = "Red";
        myCar.numberOfDoors = 4;

        myCar.start();
        myCar.accelerate();
        myCar.stop();
    }
}
```

In the example above, we have a `Vehicle` class with a `start()` and `stop()` method. The `Car` class extends the `Vehicle` class, inheriting its `color` property and `start()` and `stop()` methods. It also defines its unique property `numberOfDoors` and the `accelerate()` method.

Polymorphism allows objects of different classes to be treated as objects of a common superclass. It enables flexibility and code reusability. In Java, you can achieve polymorphism through method overriding.

```java
public class Vehicle {
    String color;

    public void start() {
        System.out.println("Vehicle started!");
    }

    public void stop() {
        System.out.println("Vehicle stopped!");
    }
}

public class Car extends Vehicle {
    int numberOfDoors;

    @Override
    public void start() {
        System.out.println("Car started with a key!");
    }

    public void accelerate() {
        System.out.println("Car accelerated!");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myVehicle = new Car();
        myVehicle.start(); // Calls the overridden start() method in the Car class
        myVehicle.stop(); // Calls the stop() method in the Vehicle class
    }
}
```

In the above example, we create a `Vehicle` object `myVehicle` and initialize it with a `Car` object. When we call the `start()` method on `myVehicle`, it executes the overridden `start()` method in the `Car` class.

## Encapsulation in Java

Encapsulation is a mechanism used to hide the internal details of an object and provide controlled access to its properties and methods. In Java, encapsulation can be achieved by using access specifiers such as `private`, `protected`, and `public`.

```java
public class Car {
    private String color; // private property

    public String getColor() { // public getter
        return color;
    }

    public void setColor(String color) { // public setter
        this.color = color;
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.setColor("Red");
        System.out.println(myCar.getColor());
    }
}
```

In the above example, the `color` property of the `Car` class is declared as private, which means it can only be accessed within the class. We provide a public getter (`getColor()`) and setter (`setColor()`) methods to access and modify the `color` property from outside the class.

## Conclusion

Object-oriented programming is a powerful paradigm that provides modularity, reusability, and scalability to your code. Java's support for OOP concepts such as classes, objects, inheritance, polymorphism, and encapsulation makes it an excellent choice for building robust and maintainable applications.

#Java #OOP