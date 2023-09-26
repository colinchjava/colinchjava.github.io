---
layout: post
title: "Overloading of method call operator in Java"
description: " "
date: 2023-09-26
tags: [methodoverloading]
comments: true
share: true
---

In Java, there is no direct operator overloading. However, you can simulate the behavior of operator overloading for method calls using the concept of *functional interfaces* and *lambda expressions*.

Functional interfaces are interfaces that have exactly one abstract method. They are mainly used to represent lambda expressions and method references.

To simulate the overloading of the method call operator, you can define a functional interface with a method that matches the signature of the operator you want to overload. Then, you can create multiple implementations of this functional interface to achieve the desired behavior.

Here's an example that demonstrates how to overload the method call operator in Java:

```java
@FunctionalInterface
interface MethodCallOperator {
    void apply();
}

class OverloadedMethods {
    void method1() {
        System.out.println("Method 1 is called");
    }
    
    void method2() {
        System.out.println("Method 2 is called");
    }
}

public class Main {
    public static void main(String[] args) {
        OverloadedMethods obj = new OverloadedMethods();
        
        MethodCallOperator operator1 = obj::method1;
        MethodCallOperator operator2 = obj::method2;
        
        operator1.apply(); // Output: Method 1 is called
        operator2.apply(); // Output: Method 2 is called
    }
}
```

In the above example, we define a functional interface `MethodCallOperator` with a method `apply()`. We then create two implementations of this interface `operator1` and `operator2`, which refer to the methods `method1()` and `method2()` of the `OverloadedMethods` object `obj` respectively.

When we call the `apply()` method on each operator, it calls the respective method and prints the corresponding message.

By using functional interfaces and lambda expressions, we can achieve a form of method call operator overloading in Java.

#java #methodoverloading