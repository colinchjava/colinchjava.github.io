---
layout: post
title: "Switch expressions in Java 12"
description: " "
date: 2023-10-24
tags: [switch]
comments: true
share: true
---

Java 12 introduced an enhancement to the `switch` statement called switch expressions. This new feature allows us to use the `switch` statement as an expression, which means we can assign the result of the `switch` statement to a variable.

## Syntax

The syntax for switch expressions in Java 12 is as follows:

```java
variable = switch (expression) {
    case constant1 -> expression1;
    case constant2, constant3 -> expression2;
    // ...
    default -> expressionN;
};
```

The `variable` on the left-hand side of the assignment operator (`=`) is assigned the value of the expression that matches one of the `case` constants. The `case` labels are followed by the arrow (`->`) that separates them from the corresponding expressions.

We can have multiple `case` constants separated by commas, which means they will execute the same expression. Also, unlike the traditional `switch` statement, we don't need to include a `break` statement at the end of each `case`.

The `default` keyword is used to specify the expression that is executed if none of the `case` constants match the given expression.

## Examples

Let's look at a few examples to understand how switch expressions work:

### Example 1: Assigning a value based on a condition

```java
String fruit = switch (day) {
    case "Monday" -> "Banana";
    case "Tuesday", "Wednesday" -> "Apple";
    case "Thursday" -> "Orange";
    case "Friday", "Saturday" -> "Mango";
    default -> "Unknown";
};
```

In this example, the value of `fruit` will be assigned based on the value of the `day` variable. If `day` is "Monday", the value will be "Banana", if `day` is "Tuesday" or "Wednesday", the value will be "Apple", and so on.

### Example 2: Returning a value from a method

```java
public int getMonthNumber(String month) {
    return switch (month) {
        case "January" -> 1;
        case "February" -> 2;
        case "March" -> 3;
        // ...
        default -> -1;
    };
}
```

In this example, the `getMonthNumber` method returns the corresponding number for the given month name. If the month is not recognized, it returns -1.

## Benefits of Switch Expressions

Switch expressions provide several benefits over the traditional `switch` statement:

- They improve code readability by allowing us to write concise and expressive code.
- They allow us to perform complex operations within the `switch` statement, including calculations, method calls, and even other nested `switch` expressions.
- They are more flexible and eliminate the need for the `break` statement, resulting in less error-prone code.
- They can be used as a normal expression, which means they can be assigned to a variable or used inside other expressions.

## Conclusion

Switch expressions in Java 12 are a powerful enhancement to the `switch` statement, allowing us to write more concise and flexible code. They provide improved readability and allow us to perform complex operations within the `switch` statement itself. It's a valuable addition to the Java language and a feature worth exploring in your projects.

**References:**
- [JEP 325: Switch Expressions (Standard) in Java SE 12](https://openjdk.java.net/jeps/325)
- [Java 12 Documentation](https://docs.oracle.com/en/java/javase/12/)
  
#java #switch-expression