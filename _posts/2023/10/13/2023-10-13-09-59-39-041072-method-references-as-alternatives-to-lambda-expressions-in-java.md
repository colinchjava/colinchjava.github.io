---
layout: post
title: "Method references as alternatives to lambda expressions in Java"
description: " "
date: 2023-10-13
tags: [MethodReferences]
comments: true
share: true
---

In Java, lambda expressions have become a popular feature for providing a concise and expressive way to write inline functions. However, there are cases where lambda expressions can be replaced with method references, providing an even simpler and more readable syntax.

Method references allow you to refer to an existing method by its name, without invoking it. They can be used in place of lambda expressions when the lambda expression simply calls a method with the same arguments as the lambda itself.

There are four types of method references in Java:

## 1. Reference to a static method

You can refer to a static method using the class name followed by `::` and the method name. This is particularly useful when the lambda expression is a one-liner that only calls a static method.

```java
// Lambda expression
Function<Integer, String> lambda = (n) -> String.valueOf(n);

// Equivalent method reference
Function<Integer, String> methodRef = String::valueOf;
```

## 2. Reference to an instance method of a particular object

You can refer to an instance method using the object name followed by `::` and the method name. This is useful when the lambda expression has a single parameter and simply passes it to an instance method.

```java
// Lambda expression
Predicate<String> lambda = (str) -> str.isEmpty();

// Equivalent method reference
Predicate<String> methodRef = String::isEmpty;
```

## 3. Reference to an instance method of an arbitrary object of a particular type

You can refer to an instance method of any object of a specific type using the type name followed by `::` and the method name. This is helpful when the lambda expression takes multiple parameters and the instance method of any object of that type can be invoked with those arguments.

```java
// Lambda expression
BiFunction<String, String, Boolean> lambda = (str1, str2) -> str1.equals(str2);

// Equivalent method reference
BiFunction<String, String, Boolean> methodRef = String::equals;
```

## 4. Reference to a constructor

You can refer to a constructor using the class name followed by `new`. This is useful when the lambda expression constructs a new object using a constructor.

```java
// Lambda expression
Supplier<List<String>> lambda = () -> new ArrayList<>();

// Equivalent method reference
Supplier<List<String>> methodRef = ArrayList::new;
```

Method references not only simplify the code by providing a shorter syntax, but they also improve readability, making the code easier to understand. However, it's important to consider the context and requirements of your code to decide whether to use a lambda expression or a method reference.

For further information, you can refer to the [Java documentation on method references](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html).

**#Java #MethodReferences**