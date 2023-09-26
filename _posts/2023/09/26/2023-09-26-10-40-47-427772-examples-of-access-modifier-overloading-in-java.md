---
layout: post
title: "Examples of access modifier overloading in Java"
description: " "
date: 2023-09-26
tags: [Java, AccessModifiers]
comments: true
share: true
---

In Java, access modifiers are keywords used to specify the level of access or visibility of classes, methods, and variables. These modifiers play a crucial role in encapsulation and ensuring code integrity. Java offers four types of access modifiers: public, private, protected, and default (also known as package-private).

When it comes to overloading in Java, access modifiers can be overloaded just like methods and constructors. Overloading refers to having multiple methods or constructors with the same name but different parameters. This allows you to create more flexible and reusable code by providing various ways to interact with the same functionality.

Let's explore an example of how you can overload access modifiers in Java:

```java
public class AccessModifiersExample {
    
    // Public method with no arguments
    public void printMessage() {
        System.out.println("This is a public method with no arguments");
    }
    
    // Public method with a string argument
    public void printMessage(String message) {
        System.out.println("Message: " + message);
    }
    
    // Private method with an integer argument
    private void printNumber(int number) {
        System.out.println("Number: " + number);
    }
    
    // Protected method with a double argument
    protected void printDecimal(double decimal) {
        System.out.println("Decimal: " + decimal);
    }
    
    // Default method with a boolean argument
    void printBoolean(boolean value) {
        System.out.println("Boolean: " + value);
    }
}
```

In the above example, we have a class named `AccessModifiersExample` with five methods. Each method has a different access modifier: public, private, protected, and default.

The `printMessage()` method is overloaded twice, once with no arguments and once with a `String` argument. Both versions of the method have a public access modifier, allowing them to be accessed from any class.

The `printNumber()` method is overloaded with a private access modifier, meaning it can only be accessed within the same class.

The `printDecimal()` method is overloaded with a protected access modifier, allowing it to be accessed from the same package and any subclass of `AccessModifiersExample`.

The `printBoolean()` method uses the default access modifier, which means it can be accessed only from classes within the same package.

Remember that when overloading methods, the access modifier does not directly affect the overloading itself. The access modifier determines the visibility of the method in different scenarios.

By using different access modifiers during method overloading, you can control how different versions of methods are accessed and used by other classes. This provides flexibility and supports encapsulation principles in Java.

#Java #AccessModifiers #Overloading