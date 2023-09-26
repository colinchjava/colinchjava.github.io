---
layout: post
title: "Overloading arithmetic operators in Java"
description: " "
date: 2023-09-26
tags: [OperatorOverloading]
comments: true
share: true
---

In Java, operators like `+`, `-`, `*`, and `/` have predefined functionalities for different data types. However, Java also allows us to *overload* these operators, which means we can define a custom functionality for these operators with our own custom data types.

To overload an arithmetic operator in Java, we need to follow a few rules:

1. The operator must be overloaded in a class.
2. The class must define the operator method with the same name as the operator.
3. The operator method must have the `public` access modifier.

Let's take an example where we want to overload the `+` operator to add two custom objects of a class.

```java
public class CustomObject {
    private int value;

    public CustomObject(int value) {
        this.value = value;
    }

    public CustomObject add(CustomObject obj) {
        int sum = value + obj.value;
        return new CustomObject(sum);
    }
}

public class Main {
    public static void main(String[] args) {
        CustomObject obj1 = new CustomObject(5);
        CustomObject obj2 = new CustomObject(10);
        CustomObject sum = obj1.add(obj2);
        
        System.out.println("Sum: " + sum.getValue());
    }
}
```

In this example, we have created a `CustomObject` class with a private variable `value`. We have defined a method `add` that takes another `CustomObject` as a parameter, adds the values of both objects, and returns a new `CustomObject` with the sum of the values.

In the `Main` class, we create two `CustomObject` instances `obj1` and `obj2`. We then call the `add` method on `obj1` and pass `obj2` as a parameter. The result is stored in the `sum` variable, which is then printed to the console using the `getValue` method.

By overloading the `+` operator, we can use it to add two `CustomObject` instances and get the desired output.

To summarize, operator overloading in Java allows us to redefine the behavior of predefined operators, enabling us to create more intuitive and convenient code. However, it's important to use operator overloading judiciously and consider its impact on code readability and maintainability.

#Java #OperatorOverloading