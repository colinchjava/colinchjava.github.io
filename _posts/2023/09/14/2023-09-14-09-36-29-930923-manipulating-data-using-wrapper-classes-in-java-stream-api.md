---
layout: post
title: "Manipulating data using wrapper classes in Java stream API"
description: " "
date: 2023-09-14
tags: [StreamAPI, DataManipulation]
comments: true
share: true
---

Java Stream API provides a powerful set of tools for manipulating data. One of the key components of the Stream API is the ability to use wrapper classes to perform operations on data elements. In this blog post, we will explore how to manipulate data using wrapper classes in Java Stream API.

## Using Wrapper Classes in Stream API

In Java, wrapper classes are used to provide a convenient way to work with primitive data types as objects. This allows us to use the methods provided by the wrapper classes to perform various operations on the data elements in a Stream.

Let's consider a simple example where we have a list of integers and we want to transform each element of the list by adding a constant value to it.

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        List<Integer> transformedNumbers = numbers.stream()
                .map(integer -> integer + 10) // adding a constant value of 10
                .collect(Collectors.toList());

        System.out.println(transformedNumbers); // Output: [11, 12, 13, 14, 15]
    }
}
```

In the code above, we first create a list of integers using the `Arrays.asList` method. We then use the `stream` method on the `numbers` list to obtain a stream of elements. We use the `map` function to perform the transformation on each element by adding 10 to it. Finally, we collect the transformed elements back into a list using the `collect` method.

## Applying Operations with Wrapper Classes

Wrapper classes provide a wide range of methods that allow us to perform various operations on data elements in a Stream. Here are a few examples:

- **Filtering**: We can use methods such as `filter` to select elements based on certain criteria. For example, we can filter out all even numbers from a list of integers.

- **Sorting**: Wrapper classes provide sorting methods like `sorted` to sort the elements in a Stream based on a specific ordering.

- **Aggregation**: Methods like `sum`, `avg`, `min`, and `max` can be used to compute aggregate values from elements in a Stream.

## Conclusion

Wrapper classes in Java Stream API provide a powerful way to manipulate data elements in a Stream. By using these wrapper classes and their methods, we can easily apply operations, transform data, and perform various manipulations on the elements of a Stream.

#Java #StreamAPI #DataManipulation