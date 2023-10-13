---
layout: post
title: "Capturing variables in lambda expressions in Java"
description: " "
date: 2023-10-13
tags: [LambdaExpressions]
comments: true
share: true
---

Lambda expressions introduced in Java 8 have made writing functional-style code more concise and expressive. One of the features of lambda expressions is the ability to capture variables from the surrounding scope. In this blog post, we'll explore how variable capturing works in lambda expressions in Java.

## What is Variable Capturing?

Variable capturing allows lambda expressions to access variables from the outer scope in which they are defined. In other words, if a variable is declared outside the lambda expression, it can still be accessed within the lambda body.

## Accessing Local Variables

Lambda expressions can only access local variables that are effectively final or effectively final. An effectively final variable is one whose value does not change after it is initialized. This means that you can use variables that are declared as final, or variables that are implicitly final (not explicitly declared as final but whose value is never changed).

Here's an example to illustrate this:

```java
public class VariableCaptureExample {
    public static void main(String[] args) {
        int x = 10; // effectively final variable

        Runnable runnable = () -> {
            System.out.println("Value of x: " + x);
        };

        x = 20; // changing the value of x

        runnable.run(); // prints "Value of x: 20"
    }
}
```

In this example, we have a variable `x` declared as 10. Even though we change the value of `x` to 20 before executing the `run` method of the lambda expression, it still prints the updated value of `x`. This demonstrates that lambda expressions capture the value of the variable at the time the lambda expression is created.

## Modifying Captured Variables

Lambda expressions can capture variables, but they cannot modify them unless the variables are declared as `final` or effectively final. Attempting to modify a captured variable that is not effectively final will result in a compilation error.

```java
public class VariableCaptureExample {
    public static void main(String[] args) {
        int x = 10;

        Runnable runnable = () -> {
            x++; // compilation error: variable x is not effectively final
        };

        runnable.run();
    }
}
```

In this example, if we try to modify the captured variable `x` inside the lambda expression, it results in a compilation error since `x` is not effectively final.

## Conclusion

Variable capturing allows lambda expressions in Java to access variables from the outer scope in which they are defined. However, these variables must be effectively final or effectively final. Understanding how variable capturing works is essential when working with lambda expressions effectively.

By using lambda expressions and variable capturing, you can write more functional and concise code in Java.

I hope this blog post provided you with a good understanding of capturing variables in lambda expressions in Java.

Happy coding! #Java #LambdaExpressions