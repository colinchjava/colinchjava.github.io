---
layout: post
title: "How to achieve multiple inheritance using interfaces in Java"
description: " "
date: 2023-09-26
tags: [Java, Inheritance]
comments: true
share: true
---

In Java, multiple inheritance is not allowed between classes. However, we can achieve the same effect through the use of interfaces. Interfaces allow a class to inherit multiple behaviors from different interfaces, effectively simulating multiple inheritance.

To demonstrate this, let's consider an example scenario where we have two interfaces: `Walkable` and `Swimmable`.

### Defining the Interfaces

First, let's define the two interfaces:

```java
public interface Walkable {
    void walk();
}

public interface Swimmable {
    void swim();
}
```

### Implementing the Interfaces

Next, we'll create a class called `Human` that implements both interfaces:

```java
public class Human implements Walkable, Swimmable {
    public void walk() {
        System.out.println("Walking...");
    }

    public void swim() {
        System.out.println("Swimming...");
    }

    // Additional methods and members specific to the Human class
}
```

### Using Multiple Inheritance

Now, let's see how we can use the `Human` class to utilize the behavior from both the `Walkable` and `Swimmable` interfaces:

```java
public class Main {
    public static void main(String[] args) {
        Human john = new Human();
        john.walk(); // Output: Walking...
        john.swim(); // Output: Swimming...
    }
}
```

In the above example, the `Human` class implements both the `Walkable` and `Swimmable` interfaces. As a result, we can create an instance of the `Human` class and use both the `walk()` and `swim()` methods, achieving the effect of multiple inheritance.

By using interfaces, we can define multiple behaviors and achieve a form of multiple inheritance in Java. It's important to note that this approach allows a class to inherit multiple behaviors, but not the state or implementation of the interfaces.

#Java #Inheritance