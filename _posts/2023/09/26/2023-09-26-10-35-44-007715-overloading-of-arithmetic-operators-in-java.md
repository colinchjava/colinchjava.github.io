---
layout: post
title: "Overloading of arithmetic operators in Java"
description: " "
date: 2023-09-26
tags: [Java, ArithmeticOperators]
comments: true
share: true
---

In Java, you can overload arithmetic operators such as `+`, `-`, `*`, `/`, and `%` to work with custom classes. This allows you to define how these operators behave when applied to objects of your custom class. 

To overload an arithmetic operator, you need to define a method with the same name as the operator and annotate it with the `@Override` annotation. The signature of the method should match the expected arguments and return type of the operator.

Here's an example of overloading the `+` operator for a custom `Fraction` class that represents a fraction:

```java
public class Fraction {
    private int numerator;
    private int denominator;

    public Fraction(int numerator, int denominator) {
        this.numerator = numerator;
        this.denominator = denominator;
    }

    public Fraction add(Fraction other) {
        int num = this.numerator * other.denominator + other.numerator * this.denominator;
        int den = this.denominator * other.denominator;
        return new Fraction(num, den);
    }

    @Override
    public String toString() {
        return numerator + "/" + denominator;
    }
}
```

In the above code, we define the `add` method to perform addition of two `Fraction` objects. We calculate the new numerator and denominator of the resulting fraction using the addition formula for fractions.

Now, we can use the overloaded `+` operator to add two `Fraction` objects:

```java
Fraction f1 = new Fraction(1, 2);
Fraction f2 = new Fraction(3, 4);
Fraction result = f1.add(f2);
System.out.println(result); // Output: 5/4

```

By overloading the `+` operator, we are able to perform addition between two `Fraction` objects using a more intuitive syntax.

In addition to the `+` operator, you can apply the same overloading concept to other arithmetic operators such as `-`, `*`, `/`, and `%`. This allows you to define customized behavior for these operators based on the requirements of your class.

#Java #ArithmeticOperators