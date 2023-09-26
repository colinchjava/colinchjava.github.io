---
layout: post
title: "Overloading instance methods in Java"
description: " "
date: 2023-09-26
tags: []
comments: true
share: true
---

In Java, method overloading allows us to define multiple methods with the same name but with different parameter lists. This concept is known as method overloading. With method overloading, we can have methods with the same name but different behaviors depending on the arguments passed to them. 

## Syntax

The syntax for overloading an instance method in Java is as follows:

```java
public class ClassName {
    public returnType methodName(parameterList1) {
        // Method implementation
    }
    
    public returnType methodName(parameterList2) {
        // Method implementation
    }
    // Additional overloaded methods
}
```

## Example

Let's take a simple example to understand the concept of method overloading in Java. We will create a class called "Calculator" that will have overloaded methods to perform addition.

```java
public class Calculator {

    public int add(int num1, int num2) {
        return num1 + num2;
    }

    public double add(double num1, double num2) {
        return num1 + num2;
    }

    public int add(int num1, int num2, int num3) {
        return num1 + num2 + num3;
    }
}
```

In the above example, we have defined three overloaded methods with the name "add." The first method takes two integers and returns their sum, the second method takes two doubles and returns their sum, and the third method takes three integers and returns their sum.

## Usage

Now, let's see how we can use the overloaded methods in our code:

```java
public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        
        int sum1 = calculator.add(5, 10);
        System.out.println("Sum of 5 and 10 is: " + sum1);
        
        double sum2 = calculator.add(2.5, 3.5);
        System.out.println("Sum of 2.5 and 3.5 is: " + sum2);
        
        int sum3 = calculator.add(1, 2, 3);
        System.out.println("Sum of 1, 2 and 3 is: " + sum3);
    }
}
```

Output:
```
Sum of 5 and 10 is: 15
Sum of 2.5 and 3.5 is: 6.0
Sum of 1, 2 and 3 is: 6
```

As we can see from the above example, we are able to call the same method name "add" with different parameter types, and Java determines the correct method to execute based on the arguments passed.

## Conclusion

Method overloading is a powerful feature in Java that allows us to write cleaner and more reusable code. By defining methods with the same name but different parameter lists, we can provide different behaviors for our methods based on the context of their usage. It is important to note that method overloading is not limited to instance methods and can also be applied to static methods.