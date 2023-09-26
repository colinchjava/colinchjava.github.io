---
layout: post
title: "Examples of method overloading in Java"
description: " "
date: 2023-09-26
tags: [Java, MethodOverloading]
comments: true
share: true
---

Method overloading is a feature in Java that allows a class to have multiple methods with the same name but different parameters. The compiler determines which method to call based on the number and types of arguments passed during the method call. This feature helps improve code readability and maintainability. Here are some examples of method overloading in Java:

## Example 1: Addition of integers using method overloading

```java
public class Calculator {
    
    public int add(int operand1, int operand2) {
        return operand1 + operand2;
    }
    
    public int add(int operand1, int operand2, int operand3) {
        return operand1 + operand2 + operand3;
    }
    
    public double add(double operand1, double operand2) {
        return operand1 + operand2;
    }
}
```

In the above example, the `Calculator` class demonstrates method overloading for addition. The class has three `add` methods with different parameter types and counts. Based on the number and types of parameters passed, the appropriate `add` method will be called.

## Example 2: Finding the maximum of two numbers using method overloading

```java
public class MathUtils {
    
    public int max(int num1, int num2) {
        return (num1 > num2) ? num1 : num2;
    }
    
    public double max(double num1, double num2) {
        return (num1 > num2) ? num1 : num2;
    }
}
```

In this example, the `MathUtils` class demonstrates method overloading for finding the maximum of two numbers. The class has two `max` methods with different numeric parameter types. The method with the appropriate parameter type will be called based on the arguments passed.

## Conclusion

Method overloading is a powerful feature in Java that allows us to define multiple methods with the same name but different parameters. It improves code readability and allows for more flexible method calls. By understanding method overloading, you can write more concise and maintainable code in your Java applications.

#Java #MethodOverloading