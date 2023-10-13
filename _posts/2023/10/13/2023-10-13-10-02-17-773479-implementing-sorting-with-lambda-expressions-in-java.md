---
layout: post
title: "Implementing sorting with lambda expressions in Java"
description: " "
date: 2023-10-13
tags: []
comments: true
share: true
---

Sorting is a common operation in programming that allows us to arrange data in a desired order. In Java, sorting can be achieved using lambda expressions, which were introduced in Java 8. Lambda expressions provide a concise and expressive way to write functions or blocks of code that can be passed as arguments to other methods.

Lambda expressions can be used with the `Collections.sort()` method or with the `Stream.sorted()` method to sort a collection of objects. In this blog post, we will explore how to use lambda expressions for sorting in Java.

## Sorting with Lambda Expressions using Collections.sort()

To sort a collection using lambda expressions, follow these steps:

1. Create a list of objects that you want to sort. For example, let's consider a list of strings:
   
   ```java
   List<String> fruits = Arrays.asList("orange", "apple", "banana", "grape");
   ```

2. Use the `Collections.sort()` method and pass a lambda expression as the second argument. The lambda expression should define the comparison logic based on which the list will be sorted. 

   ```java
   Collections.sort(fruits, (a, b) -> a.compareTo(b));
   ```

   In this example, we are sorting the list in ascending order based on the natural order of strings.

   Alternatively, you can use the following shorter syntax:

   ```java
   Collections.sort(fruits, String::compareTo);
   ```

3. After sorting, the list will be rearranged in the desired order.

Here is the complete code:

```java
import java.util.*;

public class LambdaSortingExample {
    public static void main(String[] args) {
        List<String> fruits = Arrays.asList("orange", "apple", "banana", "grape");
        
        Collections.sort(fruits, (a, b) -> a.compareTo(b));
        
        System.out.println(fruits);
    }
}
```

The output will be:

```
[apple, banana, grape, orange]
```

## Sorting with Lambda Expressions using Stream.sorted()

Java 8 introduced the `Stream` API which provides a powerful way to perform operations on collections. To sort a collection using lambda expressions with the `Stream.sorted()` method, follow these steps:

1. Create a stream from the collection you want to sort. For example:

   ```java
   List<String> fruits = Arrays.asList("orange", "apple", "banana", "grape");
   Stream<String> stream = fruits.stream();
   ```

2. Use the `sorted()` method on the stream and pass a lambda expression as an argument. The lambda expression should define the comparison logic based on which the stream will be sorted. 

   ```java
   stream.sorted((a, b) -> a.compareTo(b));
   ```

   In this example, we are sorting the stream in ascending order based on the natural order of strings.

   Alternatively, you can use the following shorter syntax:

   ```java
   stream.sorted(String::compareTo);
   ```

3. Finally, collect the sorted elements back into a list using the `collect()` method.

   ```java
   List<String> sortedFruits = stream.sorted(String::compareTo).collect(Collectors.toList());
   ```

Here is the complete code:

```java
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class LambdaSortingExample {
    public static void main(String[] args) {
        List<String> fruits = Arrays.asList("orange", "apple", "banana", "grape");
        Stream<String> stream = fruits.stream();
        
        List<String> sortedFruits = stream.sorted(String::compareTo).collect(Collectors.toList());
        
        System.out.println(sortedFruits);
    }
}
```

The output will be:

```
[apple, banana, grape, orange]
```

That's it! You have now learned how to implement sorting with lambda expressions in Java. Lambda expressions provide a concise way to specify the comparison logic and make the code more readable.

Keep in mind that the lambda expressions used for sorting can be customized based on the specific requirements of your application. This allows for flexible and efficient sorting of collections in Java.

# References
- [Oracle Java Documentation - Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)
- [Java 8 Lambda Expressions Tutorial](https://www.baeldung.com/java-8-lambda-expressions-tips)