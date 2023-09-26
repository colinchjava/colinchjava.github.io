---
layout: post
title: "How to extend an abstract class in Java"
description: " "
date: 2023-09-26
tags: [abstractclass]
comments: true
share: true
---

In Java, an abstract class provides a blueprint for other classes to inherit from. It cannot be instantiated and may contain both concrete and abstract methods. To create a new class that extends an abstract class, follow these steps:

1. Create a new Java class file:
```java
public class MyClass extends AbstractClass {
    // Class implementation goes here
}
```
Replace `MyClass` with the desired name of your class. Also, replace `AbstractClass` with the name of the abstract class you want to extend.

2. Implement the abstract methods:
An abstract class can have one or more abstract methods that must be implemented in the concrete subclass. To implement an abstract method, use the `@Override` annotation.
```java
public class MyClass extends AbstractClass {
    @Override
    public void abstractMethod() {
        // Method implementation goes here
    }
}
```
Replace `abstractMethod` with the name of the abstract method you want to implement.

3. Add any additional functionality:
Apart from implementing abstract methods, you can add new methods, fields, or override non-abstract methods inherited from the abstract class.
```java
public class MyClass extends AbstractClass {
    @Override
    public void abstractMethod() {
        // Method implementation goes here
    }

    public void additionalMethod() {
        // Additional method implementation goes here
    }
}
```

4. Instantiate and use the subclass:
You can now create objects of the subclass and access its methods and fields.
```java
public class Main {
    public static void main(String[] args) {
        MyClass myObject = new MyClass();
        myObject.abstractMethod();
        myObject.additionalMethod();
    }
}
```

Remember to import the abstract class if it belongs to a different package.

By extending an abstract class, you have the flexibility to implement the abstract methods and add additional functionality specific to your subclass. This allows for code reusability and a structured approach to object-oriented programming in Java.

#java #abstractclass #inheritance