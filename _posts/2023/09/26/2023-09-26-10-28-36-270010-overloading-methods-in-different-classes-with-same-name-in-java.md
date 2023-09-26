---
layout: post
title: "Overloading methods in different classes with same name in Java"
description: " "
date: 2023-09-26
tags: [MethodOverloading]
comments: true
share: true
---

In Java, method overloading allows us to define multiple methods with the same name but with different parameters. This feature is useful when we want to perform similar operations on different types of data.

But what if we have two classes that both define methods with the same name and the same parameter types? Can we still achieve method overloading? The answer is yes, and in this blog post, we will explore how it can be done.

## Scenario

Let's consider a simple scenario where we have two classes: `ClassA` and `ClassB`. Both classes have a method named `calculate()` that takes two integer parameters and returns their sum.

```java
public class ClassA {
    public int calculate(int a, int b) {
        return a + b;
    }
}

public class ClassB {
    public int calculate(int a, int b) {
        return a - b;
    }
}
```

## Calling Overloaded Methods

To call the overloaded methods from different classes, we need to create objects of each class and then invoke the `calculate()` method.

```java
public class Main {
    public static void main(String[] args) {
        ClassA objA = new ClassA();
        ClassB objB = new ClassB();

        int sum = objA.calculate(5, 3);
        int difference = objB.calculate(5, 3);

        System.out.println("Sum: " + sum);
        System.out.println("Difference: " + difference);
    }
}
```

## Output

The output of the above code will be:

```
Sum: 8
Difference: 2
```

## Conclusion

In Java, we can overload methods with the same name in different classes by simply defining the methods with the same name and parameter types in each class. This allows us to achieve method overloading even when the methods are defined in different classes.

By leveraging this feature, we can write cleaner and more modular code, making our programs more maintainable and easier to understand.

#Java #MethodOverloading #Programming