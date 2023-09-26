---
layout: post
title: "How to implement multiple interfaces in Java"
description: " "
date: 2023-09-26
tags: [Interfaces]
comments: true
share: true
---

In Java, a class can implement multiple interfaces by separating them with commas in the `implements` clause. This allows the class to inherit and implement the methods defined in each interface. Implementing multiple interfaces is useful when a class needs to provide different behaviors or functionalities from multiple sources.

Let's look at an example to see how to implement multiple interfaces in Java:

```java
public interface Flyable {
    void fly();
}

public interface Swimmable {
    void swim();
}

public class Bird implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Flying...");
    }
  
    @Override
    public void swim() {
        System.out.println("Swimming...");
    }
  
    // Other methods specific to Bird class
}

public class Main {
    public static void main(String[] args) {
        Bird bird = new Bird();
        bird.fly(); // Output: Flying...
        bird.swim(); // Output: Swimming...
    }
}
```

In the above example, we have two interfaces `Flyable` and `Swimmable`. Both interfaces have a single method defined. The `Bird` class implements both interfaces using the `implements` keyword. It provides the implementation for the `fly()` and `swim()` methods.

In the `Main` class, we create an instance of the `Bird` class and call the `fly()` and `swim()` methods on it. Since the `Bird` class implements both interfaces, it can perform both flying and swimming actions.

In summary, implementing multiple interfaces in Java allows a class to inherit and provide the functionality defined in each interface it implements. This enables the class to support multiple behaviors and fulfill the requirements of different interfaces.

#Java #Interfaces