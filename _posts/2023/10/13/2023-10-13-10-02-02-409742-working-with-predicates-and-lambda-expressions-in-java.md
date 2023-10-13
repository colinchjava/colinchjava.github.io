---
layout: post
title: "Working with predicates and lambda expressions in Java"
description: " "
date: 2023-10-13
tags: [examples]
comments: true
share: true
---

In Java, predicates and lambda expressions are powerful features that allow developers to write cleaner and more concise code. Predicates are functional interfaces that represent a boolean-valued function, which can be used to perform filtering, searching, or any other operation that requires evaluating a condition. Lambda expressions, on the other hand, allow us to create anonymous functions in a more compact and expressive way.

## Using Predicates

To work with predicates in Java, we need to import the `java.util.function.Predicate` interface. The `Predicate` interface defines a single abstract method `test(T t)` that takes an argument of type `T` and returns a boolean value.

Here's an example that demonstrates how to use predicates to filter a list of integers:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);
        numbers.add(4);
        numbers.add(5);

        Predicate<Integer> evenPredicate = number -> number % 2 == 0;
        List<Integer> evenNumbers = filter(numbers, evenPredicate);

        System.out.println("Even numbers: " + evenNumbers);
    }

    public static List<Integer> filter(List<Integer> list, Predicate<Integer> predicate) {
        List<Integer> result = new ArrayList<>();
        for (Integer number : list) {
            if (predicate.test(number)) {
                result.add(number);
            }
        }
        return result;
    }
}
```

In this example, we define a predicate `evenPredicate` using a lambda expression that tests whether a number is even. We then use the `filter` method to filter out the even numbers from the `numbers` list using the `evenPredicate`. The resulting list `evenNumbers` contains only the numbers that satisfy the predicate.

## Lambda Expressions

Lambda expressions provide a concise way to create anonymous functions. They are commonly used with functional interfaces, such as predicates, to perform operations on collections or streams.

Here's an example that demonstrates the usage of lambda expressions with predicates to filter a list of strings:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class LambdaExpressionExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("John");
        names.add("Jane");
        names.add("David");
        names.add("Alice");
        names.add("Michael");

        Predicate<String> startsWithJ = name -> name.startsWith("J");
        List<String> filteredNames = filter(names, startsWithJ);

        System.out.println("Filtered names: " + filteredNames);
    }

    public static List<String> filter(List<String> list, Predicate<String> predicate) {
        List<String> result = new ArrayList<>();
        for (String name : list) {
            if (predicate.test(name)) {
                result.add(name);
            }
        }
        return result;
    }
}
```

In this example, we define a predicate `startsWithJ` using a lambda expression that tests whether a string starts with the letter "J". We then use the `filter` method to filter out the names that satisfy the `startsWithJ` predicate.

## Conclusion

Working with predicates and lambda expressions in Java allows us to write more readable and concise code. Predicates enable us to define conditions that can be used for filtering or evaluating data, while lambda expressions provide a way to create anonymous functions in a more compact syntax. By leveraging these features, developers can enhance their Java code and make it more efficient and expressive.

**References:**

- [Oracle Java Documentation on Predicate](https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html)
- [Oracle Java Documentation on Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#examples)