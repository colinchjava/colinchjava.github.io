---
layout: post
title: "Syntax of lambda expressions in Java"
description: " "
date: 2023-10-13
tags: [lambdas]
comments: true
share: true
---

Lambda expressions were introduced in Java 8 to facilitate functional programming and make the code more concise and readable. They allow us to treat functions as method arguments or code as data.

The syntax of a lambda expression consists of three parts:

1. **Parameter List:** This is the list of parameters that the lambda expression takes as input. It can be empty if the expression doesn't require any arguments. For example, `(int a, int b)` or `()`.
 
2. **Arrow Token:** The arrow token `->` separates the parameter list from the body of the lambda expression. It signifies that the input parameters are used to define the behavior of the expression. 

3. **Body:** This is the actual implementation of the lambda expression. It can be a single statement or a block of statements enclosed in curly braces. If the body is a single statement, curly braces can be omitted. For example, `a + b` or `{ System.out.println("Hello"); return a + b; }`.

Here is the general syntax of a lambda expression:

```java
(Parameter List) -> { Body }
```

Now let's see a few examples of lambda expressions:

1. Addition of two numbers:
```java
(int a, int b) -> a + b
```
This lambda expression takes two integer parameters `a` and `b`, and returns their sum.

2. Checking if a number is even:
```java
(int number) -> number % 2 == 0
```
This lambda expression takes an integer parameter `number` and returns `true` if the number is even, otherwise `false`.

3. Printing a message:
```java
() -> System.out.println("Hello, World!")
```
This lambda expression doesn't take any parameters and simply prints "Hello, World!".

Lambda expressions can also be used with functional interfaces, which are interfaces that define a single abstract method. They provide the target type for lambda expressions in Java.

With the introduction of lambda expressions, Java has become more expressive and allows developers to write concise and readable code.

**References:**
- [Oracle Java Tutorial - Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)

#java #lambdas