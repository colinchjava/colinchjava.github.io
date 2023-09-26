---
layout: post
title: "Dynamic binding in abstract classes in Java"
description: " "
date: 2023-09-26
tags: [abstractclasses]
comments: true
share: true
---

In object-oriented programming, dynamic binding refers to the mechanism that allows different methods to be dynamically invoked based on the actual type of the object at runtime. In Java, dynamic binding is achieved through the use of inheritance and polymorphism.

Abstract classes in Java provide a great way to define common behavior for a group of related classes. An abstract class can have both abstract and non-abstract methods. 

Let's take a closer look at how dynamic binding works in the context of abstract classes in Java.

## The Abstract Class

To create an abstract class in Java, simply use the `abstract` keyword before the class declaration. Abstract classes cannot be instantiated directly, but they can be extended by other classes.

Here's an example of an abstract class called `Animal`:

```java
public abstract class Animal {
    public abstract void makeSound();
    
    public void breathe() {
        System.out.println("Breathing...");
    }
}
```

In this example, `Animal` is an abstract class that has an abstract method `makeSound()` and a non-abstract method `breathe()`. The `makeSound()` method is declared as abstract because we want each concrete subclass to provide its own implementation.

## Dynamic Binding with Abstract Methods

When a concrete subclass extends an abstract class, it must provide implementations for all the abstract methods defined in the abstract class. This is where dynamic binding comes into play.

Let's create a concrete class `Dog` that extends the `Animal` abstract class:

```java
public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof woof!");
    }
}
```

In this example, `Dog` is a subclass of `Animal` and it overrides the `makeSound()` method to provide its own implementation.

## Dynamic Binding at Runtime

Now, let's see dynamic binding in action:

```java
public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.makeSound(); // Outputs "Woof woof!"
        
        animal = new Cat();
        animal.makeSound(); // Outputs "Meow!"
    }
}
```

In this example, we create an instance of `Dog` and assign it to an `Animal` reference variable. When we invoke the `makeSound()` method on this object, the overridden `makeSound()` method in the `Dog` class is dynamically invoked, so it outputs "Woof woof!".

Similarly, if we create an instance of `Cat` and assign it to the same `Animal` reference variable, the overridden `makeSound()` method in the `Cat` class will be dynamically invoked, so it outputs "Meow!".

Dynamic binding allows us to treat objects of different subclasses in a uniform way by using a common abstract class reference. This flexibility and polymorphism are fundamental concepts in object-oriented programming.

# #java #abstractclasses #dynamicbinding