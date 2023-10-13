---
layout: post
title: "Comparing lambda expressions in Java"
description: " "
date: 2023-10-13
tags: [lambdas]
comments: true
share: true
---

Lambda expressions were introduced in Java 8 to simplify the process of writing functional interfaces. They allow you to write more concise code by eliminating the need for anonymous inner classes. In this blog post, we will compare different ways to write lambda expressions in Java.

## What is a Lambda Expression?

A lambda expression is a concise way to represent a functional interface. It consists of a set of parameters, a lambda operator `->`, and a body. The body can be a single expression or a block of code. Lambda expressions are used to implement functional interfaces, which are interfaces with only one abstract method.

## Syntax and Examples

### Single Parameter

When a lambda expression has a single parameter, you can omit the parentheses around the parameter. 

The following example illustrates a lambda expression that takes a `String` parameter and prints it to the console:

```java
(str) -> System.out.println(str);
```

### Multiple Parameters

If the lambda expression has multiple parameters, you need to enclose them in parentheses.

The following example shows a lambda expression that takes two `int` parameters, multiplies them, and returns the result:

```java
(a, b) -> a * b;
```

### Body with a Single Expression

If the body of the lambda expression contains a single expression, you can omit the curly braces `{}`. The expression's result is implicitly returned.

Here's an example of a lambda expression that adds two numbers and returns the sum:

```java
(a, b) -> a + b;
```

### Body with Multiple Statements

If the body of the lambda expression contains multiple statements, you must enclose them in curly braces `{}`. You also need to use the `return` keyword to return a value explicitly.

As an example, consider a lambda expression that calculates the average of an array of integers:

```java
array -> {
    int sum = 0;
    for (int num : array) {
        sum += num;
    }
    return sum / array.length;
};
```

## Functional Interfaces and Type Inference

To use a lambda expression, you need a functional interface that matches the lambda's signature. A functional interface is an interface with only one abstract method.

Java provides a set of built-in functional interfaces, such as `Predicate`, `Function`, and `Consumer`, among others. You can also define your own functional interfaces.

In most cases, you don't need to explicitly specify the functional interface's type when using a lambda expression. Java can infer it based on the lambda expression's context.

For example, consider the following code that uses the `Predicate` functional interface to filter a list of integers:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> evenNumbers = numbers.stream()
                                   .filter(num -> num % 2 == 0)
                                   .collect(Collectors.toList());
```

In this example, the lambda expression `num -> num % 2 == 0` is automatically inferred to be of type `Predicate<Integer>`.

## Conclusion

Lambda expressions provide a concise and expressive way to write code in Java. They eliminate the need for verbose anonymous inner classes and make working with functional interfaces more intuitive. By understanding the syntax and examples of lambda expressions, you can leverage their power to write cleaner and more readable code.

For more information on lambda expressions and functional interfaces in Java, refer to the [official documentation](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html).

#java #lambdas