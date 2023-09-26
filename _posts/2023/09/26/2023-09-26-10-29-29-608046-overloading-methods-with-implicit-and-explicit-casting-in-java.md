---
layout: post
title: "Overloading methods with implicit and explicit casting in Java"
description: " "
date: 2023-09-26
tags: [methodoverloading]
comments: true
share: true
---

Java, being a statically typed language, allows you to overload methods based on different parameter types. This means that you can have multiple methods with the same name but different parameter types. In addition, Java provides implicit and explicit casting mechanisms that allow you to convert one data type to another.

## Implicit Casting

Implicit casting, also known as widening conversion, occurs when you convert a smaller data type to a larger data type. For example, converting an integer to a double.

Let's say we have a class called `Calculation` with two overloaded methods: `add(int a, int b)` and `add(double a, double b)`. 

```java
public class Calculation {

    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```

If we invoke the `add` method with two integer parameters, the compiler will automatically cast the `int` values to `double` and call the second overloaded method because `double` is a wider data type than `int`.

```java
Calculation calculation = new Calculation();
System.out.println(calculation.add(5, 3));
```
Output: 8.0

## Explicit Casting

Explicit casting, also known as narrowing conversion, occurs when you convert a larger data type to a smaller data type. For example, converting a double to an integer.

Let's modify our `Calculation` class to include a method that takes a `double` parameter and casts it to an `int`.

```java
public class Calculation {

    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(double a) {
        return (int) a;
    }
}
```

If we invoke the `add` method with a `double` parameter, the compiler will call the method with the explicitly cast `int` parameter.

```java
Calculation calculation = new Calculation();
System.out.println(calculation.add(4.6));
```
Output: 4

In this case, the decimal part of the `double` number is truncated, resulting in an output of 4.

## Conclusion

Overloading methods based on implicit and explicit casting in Java allows you to provide flexibility while working with different data types. Implicit casting automatically widens the data type, while explicit casting allows you to narrow the data type. Understanding these concepts will help you write more flexible and efficient code.

#java #methodoverloading