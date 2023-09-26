---
layout: post
title: "How to create an abstract class in Java"
description: " "
date: 2023-09-26
tags: [AbstractClass]
comments: true
share: true
---

In object-oriented programming, an *abstract class* serves as a blueprint for other classes and cannot be instantiated on its own. It provides a common set of attributes and methods that can be inherited by its subclasses. Abstract classes are used to define common behaviors or characteristics that subclasses should implement.

To create an abstract class in Java, follow these steps:

1. Start by defining the class with the `abstract` keyword.
2. Declare any attributes or variables specific to the abstract class.
3. Define any abstract methods that subclasses must implement.
   - Use the `abstract` keyword before the method declaration, without providing a body.
4. Implement any non-abstract methods in the abstract class.
   - Non-abstract methods can provide default implementations that subclasses can inherit.
5. Subclasses that extend the abstract class must implement all abstract methods.

Here is an example of creating an abstract class in Java:

```java
public abstract class Animal {
    protected String name;
    
    // Abstract method
    public abstract void makeSound();
    
    // Non-abstract method
    public void sleep() {
        System.out.println("Zzzz...");
    }
    
    // Constructor
    public Animal(String name) {
        this.name = name;
    }
}
```

In this example, the `Animal` class is declared as an abstract class. It has a protected `name` attribute and an abstract method `makeSound()`. The non-abstract method `sleep()` provides a default implementation for all animals. The constructor `Animal(String name)` sets the value of the `name` attribute.

You can then create concrete subclasses that extend the abstract `Animal` class and implement the abstract method `makeSound()`:

```java
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    public void makeSound() {
        System.out.println("Woof!");
    }
}

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    public void makeSound() {
        System.out.println("Meow!");
    }
}
```

In this example, the `Dog` and `Cat` classes extend the `Animal` abstract class and implement the `makeSound()` method.

Remember that abstract classes cannot be instantiated directly, but they serve as a blueprint for creating related subclasses.

#Java #AbstractClass